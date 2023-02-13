win32event .MsgWaitForMultipleObjects   

[Link](http://timgolden.me.uk/pywin32-docs/win32event.html)

int = MsgWaitForMultipleObjects(handleList, bWaitAll , milliseconds , wakeMask )   
이벤트의 메시지가 도착하면 반환됩니다.   

- handleList : [PyHANDLE, ...]   
대기할 일련의 핸들입니다.   
- bWaitAll : 부울   
true인 경우 목록의 모든 핸들을 기다립니다.   
- milliseconds : int   
time-out interval in milliseconds   
- wakeMask : int   
대기할 입력 이벤트의 유형입니다. win32event.QS_ 상수 중 하나입니다.   

Note: that if bWaitAll is TRUE, the function will return when there is input in the queue, and all events are signalled. , If input is waiting, the result is win32event.WAIT_OBJECT_0+len(handles))


```python
import sys
 
import pythoncom
from PyQt5.QtWidgets import *
import win32event
 
 
StopEvent = win32event.CreateEvent(None, 0, 0, None)
################################################
# 테스트를 위한 메인 화면
class MyWindow(QMainWindow):
    def __init__(self):
        super().__init__()
 
 
        self.setWindowTitle("Test")
        self.setGeometry(300, 300, 300, 180)
 
        nH = 20
 
        btnStart = QPushButton('strat Pump', self)
        btnStart.move(20, nH)
        btnStart.clicked.connect(self.btnStartPump)
        nH += 50
 
        btnStop = QPushButton('stop Pump', self)
        btnStop.move(20, nH)
        btnStop.clicked.connect(self.btnStopPump)
        nH += 50
 
        btnExit = QPushButton('종료', self)
        btnExit.move(20, nH)
        btnExit.clicked.connect(self.btnExit_clicked)
        nH += 50
 
    def MessagePump(sef, timeout):
        while 1:
            rc = win32event.MsgWaitForMultipleObjects(
                [StopEvent],
                0,  # Wait for all = false, so it waits for anyone
                win32event.INFINITE, # timeout
                win32event.QS_ALLEVENTS)  # Accepts all input
 
            if rc == win32event.WAIT_OBJECT_0:
                # 나열된 첫 번째 이벤트인 StopEvent가 트리거되었으므로 종료해야 합니다
                print('stop event')
                break
 
            elif rc == win32event.WAIT_OBJECT_0 + len([StopEvent]):
                # Windows 메시지가 대기 중입니다
                print('pump')
                if pythoncom.PumpWaitingMessages():
                    break  # we received a wm_quit message
            elif rc == win32event.WAIT_TIMEOUT:
                print('timeout')
                return
            else:
                print('exception')
                raise RuntimeError("unexpected win32wait return value")
 
    def btnStartPump(self):
        self.MessagePump(5000)
        return
 
    def btnStopPump(self):
        win32event.SetEvent(StopEvent)
        return
 
 
    def btnExit_clicked(self):
        exit()
        return
 
 
if __name__ == "__main__":
    app = QApplication(sys.argv)
    myWindow = MyWindow()
    myWindow.show()
    app.exec_()

```
