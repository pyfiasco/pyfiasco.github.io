---
layout: default
title: MultiProcessing
parent: Library
grand_parent: Python
---

# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

threading 모듈 사용하기
파이썬에서 스레드를 다루는 다양한 방법이 있습니다. 파이썬 기본 모듈로는 thread와 threading 모듈이 있는데 보통 theading 모듈을 더 자주 사용합니다. 이외에도 GUI 라이브러리인 PyQt의 QThread를 사용하기도 합니다. 이장에서는 threading 모듈을 사용해서 스레드를 생성해 보겠습니다.

import threading
import time


class Worker(threading.Thread):
    def __init__(self, name):
        super().__init__()
        self.name = name            # thread 이름 지정

    def run(self):
        print("sub thread start ", threading.currentThread().getName())
        time.sleep(3)
        print("sub thread end ", threading.currentThread().getName())


print("main thread start")
for i in range(5):
    name = "thread {}".format(i)
    t = Worker(name)                # sub thread 생성
    t.start()                       # sub thread의 run 메서드를 호출

print("main thread end")
실행 결과는 다음과 같습니다. 메인 스레드가 5개의 서브 스레드를 생성하고 start 메서드를 호출하여 Worker 클래스에 정의한 run( ) 메서드를 호출합니다. 메인 스레드와 5개의 서브 스레드는 운영체제의 스케줄러에 의해 스케줄링 되면서 실행됩니다. 가장 먼저 메인 스레드가 끝나면서 'main thread end'를 출력합니다. 서브 스레드들은 0, 1, 2, 3, 4 순으로 실행됐지만 종료 순서는 조금 다른 것을 확인할 수 있습니다. 기본적으로 메인 스레드에서 서브 스레드를 생성하면 메인 스레드는 자신의 작업을 모두 마쳤더라도 서브 스레드의 작업이 종료될 때 까지 기다렸다가 서브 스레드의 작업이 모두 완료되면 종료됩니다.

main thread start
sub thread start  thread 0
sub thread start  thread 1
sub thread start  thread 2
sub thread start  thread 3
sub thread start  thread 4
main thread end
sub thread end  thread 0
sub thread end  thread 1
sub thread end sub thread end  thread 2
 thread 4
sub thread end  thread 3

Sub
Thread0
Main 
Thread
Sub
Thread4
Fork
Main
Thread
Join
Main
Thread
데몬 스레드 만들기
데몬(daemon) 스레드는 메인 스레드가 종료될 때 자신의 실행 상태와 상관없이 종료되는 서브 스레드를 의미합니다. 앞서 threading 모듈을 사용해서 메인 스레드가 서브 스레드를 생성하는 경우 메인 스레드는 서브 스레드가 모두 종료될 때까지 기다렸다가 종료하게 됩니다. 그런데 실제 프로그래밍을 하다보면 경우에 따라 메인 스레드가 종료되면 모두 서브스레드가 동작 여부에 상관없이 종료되어야 하는 경우가 많습니다. 예를 들어 토렌토와 같은 파일 다운로드 프로그램에서 서브 스레드를 통해 파일을 동시에 다운로드 받고 있는데 사용자가 메인 프로그램을 종료하면 파일의 다운로드 완료 여부와 상관없이 프로그램이 종료되어야 할 것입니다. 이때 서브 스레드 들은 데몬 스레드로 만들어져야 합니다. 파이썬 threading 모듈에서 데몬 스레드의 생성은 daemon 속성을 True로 변경하면 됩니다.

import threading
import time


class Worker(threading.Thread):
    def __init__(self, name):
        super().__init__()
        self.name = name            # thread 이름 지정

    def run(self):
        print("sub thread start ", threading.currentThread().getName())
        time.sleep(3)
        print("sub thread end ", threading.currentThread().getName())


print("main thread start")
for i in range(5):
    name = "thread {}".format(i)
    t = Worker(name)                # sub thread 생성
    t.daemon = True
    t.start()                       # sub thread의 run 메서드를 호출

print("main thread end")
실행 결과를 확인해보면 메인 스레드가 종료되면서 time.sleep(3)에 의해 대기 상태에 있던 서브 스레드들은 끝나기 전에 모두 종료된 것을 확인할 수 있습니다.

main thread start
sub thread start  thread 0
sub thread start  thread 1
sub thread start  thread 2
sub thread start  thread 3
sub thread start  thread 4
main thread end
Fork와 Join
이번에는 fork-join에 대해서 배우겠습니다. 다음 그림처럼 메인 스레드가 서브 스레드를 생성하는 것을 fork 라고 합니다. 두 개의 서브 스레드를 생성하는 경우 메인 스레드를 포함하여 총 3개의 스레드가 스케줄링 됩니다. join은 모든 스레드가 작업을 마칠 때까자 기다리는 것을 의미합니다. 보통 데이터를 여러 스레드를 통해서 병렬로 처리한 후 그 값들을 다시 모아서 순차적으로 처리해야할 필요가 있을 때 분할한 데이터가 모든 스레드에서 처리될 때까지 기다렸다가 메인 스레드가 다시 추후 작업을 하는 경우에 사용합니다.

main thread
sub thread
sub thead
Fork
main thread
main thread
Join

import threading
import time


class Worker(threading.Thread):
    def __init__(self, name):
        super().__init__()
        self.name = name            # thread 이름 지정

    def run(self):
        print("sub thread start ", threading.currentThread().getName())
        time.sleep(5)
        print("sub thread end ", threading.currentThread().getName())


print("main thread start")

t1 = Worker("1")        # sub thread 생성
t1.start()              # sub thread의 run 메서드를 호출

t2 = Worker("2")        # sub thread 생성
t2.start()              # sub thread의 run 메서드를 호출

t1.join()
t2.join()

print("main thread post job")
print("main thread end")
결과를 보면 t1, t2 스레드가 종료된 후 'main thread post job'이 출력된 것을 확인할 수 있습니다. 참고로 앞의 예에서는 메인스레드가 모든 실행을 완료한 후 서브스레드가 종료될 때까지 기다렸지만 이 예제에서는 join( ) 메서드가 호출되는 지점에서 기다린다는 차이가 있습니다.

main thread start
sub thread start  1
sub thread start  2
sub thread end  2
sub thread end  1
main thread post job
main thread end
반복문을 통해 여러 서브 스레드를 생성해야하는 경우에는 생성된 스레드 객체를 파이썬 리스트에 저장한 후 반복문을 이용해서 각 객체에서 join( ) 메서드를 호출할 수 있습니다.

import threading
import time


class Worker(threading.Thread):
    def __init__(self, name):
        super().__init__()
        self.name = name            # thread 이름 지정

    def run(self):
        print("sub thread start ", threading.currentThread().getName())
        time.sleep(5)
        print("sub thread end ", threading.currentThread().getName())


print("main thread start")

threads = []
for i in range(3):
    thread = Worker(i)
    thread.start()              # sub thread의 run 메서드를 호출
    threads.append(thread)


for thread in threads:
    thread.join()

print("main thread post job")
print("main thread end")
