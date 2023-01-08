---
layout: default
title: Vscode 사용법

parent: 사용메뉴얼
has_children: true
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

# Download Extensions for Visual Studio Code
- https://marketplace.visualstudio.com/vscode

# insall/delete Visual Studio Code

## Vscode install

- [Windows](https://code.visualstudio.com/docs/setup/windows)
    - 설치 위치: C:\Users\{Username}\AppData\Local\Programs\Microsoft VS Code
    - 사용자 환경변수 등록: C:\Users\neo21\AppData\Local\Programs\Microsoft VS Code\bin

## Vscode Uninstall
- 제어판에서 uninstall
    - unins000.exe 실행으로도 가능 : C:\Users\neo21\AppData\Local\Programs\Microsoft VS Code
- 파일 삭제
    %APPDATA%\Code
    %USERPROFILE%\.vscode

[ 참조 ] %APPDATA%, %USERPROFILE% 위치 확인 방법
- 파일탐색기에서 직접 입력 검색
- 명령프롬프트에서 확인

```python
$ echo %APPDATA% 
C:\Users\neo21\AppData\Roaming
$ echo %USERPROFILE%
C:\Users\neo21
```
## User and Workspace Settings
`Command Palette` (Ctrl+Shift+P) with `Preferences: Open Settings` ,(Ctrl+,)
- User Settings - Settings that apply globally to any instance of VS Code you open.
    - 설정 파일 위치: %APPDATA%\Code\User\settings.json
- Workspace Settings - Settings stored inside your workspace and only apply when the workspace is opened.
    - 작업 폴더내 .vscode/workspace.json
    작업 공간 설정은 사용자 설정보다 우선합니다.

참고 : VS Code "작업 공간"은 일반적으로 프로젝트 루트 폴더입니다. 작업 공간 설정과 디버깅 및 작업 구성은 폴더의 루트에 저장됩니다.vscode. 다중 루트 작업 영역 이라는 기능을 통해 VS Code 작업 영역에 둘 이상의 루트 폴더를 가질 수도 있습니다. 

=========================================
## Conda 가상환경 사용
1. cmd 사용환경 구축
    - 시스템 환경변수 추가
        : anaconda3, anaconda3/Library, anaconda3/Scripts 세 개의 경로를 추가한다.
    - vsc에서 Ctrl + Shift + P 를 누른 뒤 팝업되는 검색 창에 'Terminal: Select Default Profile' 선택
    - 터미널 창에서 cmd 확인 가능
2. 가상환경 만들기
    - ssl인증 않기               : conda config --set ssl_verify no
    - 가상환경 생성(폴더명: test) : conda create --name test
        - 생성 위치              : c:\Users\aaaa\Anaconda3\env\test
    - 가상환경 목록 확인          : $cond env list
    - activate                   : $conda activate 가상환경명
3. 가상환경 사용하기
    - 오른쪽 아래 상태창에서 python 버전/가상환경 확인/변경
4. 가상환경 삭제                  : conda env remove --n 가상환경이름
   

## vscode debugging 시작경로 변경

launch.json 항목 추가
"cwd": "${fileDirname}" # 현재 폴더 경로에서 디버그 시작 설정

## 자신이 작성한 모듈 노출시키기
- Reveal in File Explorer

## 파이썬 시스템 환경변수 설정
C:\Users\neo21\AppData\Local\Programs\Python\Python311
C:\Users\neo21\AppData\Local\Programs\Python\Python311\Lib   # 기본 모듈 설치 장소
C:\Users\neo21\AppData\Local\Programs\Python\Python311\DLLs

## VScode의 확장프로그램 설치 위치 : extensions
Windows : %USERPROFILE%\.vscode\extensions
Mac : ~/.vscode/extensions 또는 /Users/<user>/.vscode/extensions
Linux : ~/.vscode/extensions
vscode 모듈 설치 위치 변경



## new terminal 시작 경로 변경
설정 : Terminal>Integrated:cwd
원하는 경로 입력
=================


[Setup](https://code.visualstudio.com/docs/setup/setup-overview) - Install VS Code for your platform and configure the tool set for your development needs.

[User Interface](https://code.visualstudio.com/docs/getstarted/userinterface) - Introduction to the basic UI, commands, and features of the VS Code editor.

[Settings](https://code.visualstudio.com/docs/getstarted/settings) - Customize VS Code for how you like to work.

[Languages](https://code.visualstudio.com/docs/languages/overview) - Learn about VS Code's support for your favorite programming languages.

[Node.js](https://code.visualstudio.com/docs/nodejs/nodejs-tutorial) - This tutorial gets you quickly running and debugging a Node.js web app.

[Tips and Tricks](https://code.visualstudio.com/docs/getstarted/tips-and-tricks) - Jump right in with Tips and Tricks to become a VS Code power user.

[Azure](https://code.visualstudio.com/docs/azure/extensions) - VS Code is great for deploying your web applications to the cloud.

[Extension API](https://code.visualstudio.com/api) - Learn how to write a VS Code extension.

[Why VS Code?](https://code.visualstudio.com/docs/editor/whyvscode) - Read about the design philosophy and architecture of VS Code.

Keyboard Shortcuts

Increase your productivity with VS Code's keyboard shortcuts.

[Keyboard Shortcut Reference Sheet](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference) - Learn the commonly used keyboard shortcuts.

[Keymap Extensions](https://code.visualstudio.com/docs/getstarted/keybindings#_keymap-extensions) - Change VS Code's keyboard shortcuts to match another editor.

[Customize Keyboard Shortcuts](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-editor) - Modify the default keyboard shortcuts.

[How do I disable auto update?](https://code.visualstudio.com/docs/supporting/faq#_how-do-i-opt-out-of-vs-code-autoupdates)

[How do I disable crash reporting?](https://code.visualstudio.com/docs/supporting/faq#_how-to-disable-crash-reporting)

[How do I disable usage reporting?](https://code.visualstudio.com/docs/supporting/faq#_how-to-disable-telemetry-reporting)


=================

VS Code is lightweight and should run on most available hardware and platform versions. You can review the [System Requirements](https://code.visualstudio.com/docs/supporting/requirements) to check if your computer configuration is supported.

[Update cadence](https://code.visualstudio.com/docs/setup/setup-overview#_update-cadence)

VS Code releases a new version [each month](https://code.visualstudio.com/updates) with new features and important bug fixes. Most platforms support auto updating and you will be prompted to install the new release when it becomes available. You can also manually check for updates by running  **Help**  \>  **Check for Updates**  on Linux and Windows or running  **Code**  \>  **Check for Updates**  on macOS.

Note: You can [disable auto-update](https://code.visualstudio.com/docs/supporting/faq#_how-do-i-opt-out-of-vs-code-autoupdates) if you prefer to update VS Code on your own schedule.

[Insiders nightly build](https://code.visualstudio.com/docs/setup/setup-overview#_insiders-nightly-build)

If you'd like to try our nightly builds to see new features early or verify bug fixes, you can install our [Insiders build](https://code.visualstudio.com/insiders). The Insiders build installs side-by-side with the monthly Stable build and you can freely work with either on the same machine. The Insiders build is the same one the VS Code development team uses on a daily basis and we really appreciate people trying out new features and providing feedback.

[Portable mode](https://code.visualstudio.com/docs/setup/setup-overview#_portable-mode)

Visual Studio Code supports [Portable mode](https://en.wikipedia.org/wiki/Portable_application) installation. This mode enables all data created and maintained by VS Code to live near itself, so it can be moved around across environments, for example, on a USB drive. See the [VS Code Portable Mode](https://code.visualstudio.com/docs/editor/portable) documentation for details.

[Additional components](https://code.visualstudio.com/docs/setup/setup-overview#_additional-components)

VS Code is an editor, first and foremost, and prides itself on a small footprint. Unlike traditional IDEs that tend to include everything but the kitchen sink, you can tune your installation to the development technologies you care about. Be sure to read the [Additional Components](https://code.visualstudio.com/docs/setup/additional-components) topic after reading the platform guides to learn about customizing your VS Code installation.

[Extensions](https://code.visualstudio.com/docs/setup/setup-overview#_extensions)

VS Code [extensions](https://code.visualstudio.com/docs/editor/extension-marketplace) let third parties add support for additional:

- Languages - [C++](https://code.visualstudio.com/docs/languages/cpp), [C#](https://code.visualstudio.com/docs/languages/csharp), [Go](https://code.visualstudio.com/docs/languages/go), [Java](https://code.visualstudio.com/docs/languages/java), [Python](https://code.visualstudio.com/docs/languages/python)
- Tools - [ESLint](https://marketplace.visualstudio.com/items/dbaeumer.vscode-eslint), [JSHint](https://marketplace.visualstudio.com/items/dbaeumer.jshint) , [PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell)
- Debuggers - [PHP XDebug](https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug).
- Keymaps - [Vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim), [Sublime Text](https://marketplace.visualstudio.com/items?itemName=ms-vscode.sublime-keybindings), [IntelliJ](https://marketplace.visualstudio.com/items?itemName=k--kato.intellij-idea-keybindings), [Emacs](https://marketplace.visualstudio.com/items?itemName=hiro-sun.vscode-emacs), [Atom](https://marketplace.visualstudio.com/items?itemName=ms-vscode.atom-keybindings), [Brackets](https://marketplace.visualstudio.com/items?itemName=ms-vscode.brackets-keybindings), [Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vs-keybindings), [Eclipse](https://marketplace.visualstudio.com/items?itemName=alphabotsec.vscode-eclipse-keybindings)

Extensions integrate into VS Code's UI, commands, and task running systems so you'll find it easy to work with different technologies through VS Code's shared interface. Check out the VS Code extension [Marketplace](https://marketplace.visualstudio.com/vscode) to see what's available.

[Next steps](https://code.visualstudio.com/docs/setup/setup-overview#_next-steps)

Once you have installed and set up VS Code, these topics will help you learn more about VS Code:

- [Additional Components](https://code.visualstudio.com/docs/setup/additional-components) - Learn how to install Git, Node.js, TypeScript, and tools like Yeoman.
- [User Interface](https://code.visualstudio.com/docs/getstarted/userinterface) - A quick orientation to VS Code.
- [Basic Editing](https://code.visualstudio.com/docs/editor/codebasics) - Learn about the powerful VS Code editor.
- [Code Navigation](https://code.visualstudio.com/docs/editor/editingevolved) - Move quickly through your source code.
- [Debugging](https://code.visualstudio.com/docs/editor/debugging) - Debug your source code directly in the VS Code editor.
- [Proxy Server Support](https://code.visualstudio.com/docs/setup/network) - Configure your proxy settings.

If you'd like to get something running quickly, try the [Node.js tutorial](https://code.visualstudio.com/docs/nodejs/nodejs-tutorial) walkthrough that will have you debugging a Node.js web application with VS Code in minutes.

[Common questions](https://code.visualstudio.com/docs/setup/setup-overview#_common-questions)

[What are the system requirements for VS Code?](https://code.visualstudio.com/docs/setup/setup-overview#_what-are-the-system-requirements-for-vs-code)

We have a list of [System Requirements](https://code.visualstudio.com/docs/supporting/requirements).

[How big is VS Code?](https://code.visualstudio.com/docs/setup/setup-overview#_how-big-is-vs-code)

VS Code is a small download (\< 100 MB) and has a disk footprint of less than 200 MB, so you can quickly install VS Code and try it out.

[How do I create and run a new project?](https://code.visualstudio.com/docs/setup/setup-overview#_how-do-i-create-and-run-a-new-project)

VS Code doesn't include a traditional  **File**  \>  **New Project**  dialog or pre-installed project templates. You'll need to add [additional components](https://code.visualstudio.com/docs/setup/additional-components) and scaffolders depending on your development interests. With scaffolding tools like [Yeoman](https://yeoman.io/) and the multitude of modules available through the [npm](https://www.npmjs.com/) package manager, you're sure to find appropriate templates and tools to create your projects.

[How do I know which version I'm running?](https://code.visualstudio.com/docs/setup/setup-overview#_how-do-i-know-which-version-im-running)

On Linux and Windows, choose  **Help**  \>  **About**. On macOS, use  **Code**  \>  **About Visual Studio Code**.

[Why is VS Code saying my installation is Unsupported?](https://code.visualstudio.com/docs/setup/setup-overview#_why-is-vs-code-saying-my-installation-is-unsupported)

VS Code has detected that some installation files have been modified, perhaps by an extension. Reinstalling VS Code will replace the affected files. See our [FAQ topic](https://code.visualstudio.com/docs/supporting/faq#_installation-appears-to-be-corrupt-unsupported) for more details.

[How can I do a 'clean' uninstall of VS Code?](https://code.visualstudio.com/docs/setup/setup-overview#_how-can-i-do-a-clean-uninstall-of-vs-code)

If you want to remove all user data after [uninstalling](https://code.visualstudio.com/docs/setup/uninstall) VS Code, you can delete the user data folders Code and .vscode. This will return you to the state before you installed VS Code. This can also be used to reset all settings if you don't want to uninstall VS Code.

The folder locations will vary depending on your platform:



