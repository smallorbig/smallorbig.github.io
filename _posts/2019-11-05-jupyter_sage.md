---
title: "Resister SageMath to Jupyter Notebook"
excerpt: ""
date: 2019-11-05
categories: 
- Linux
tags: 
- server, 
- jupyter, 
- sage
---


# Introduction

MacOS에 Anaconda를 설치하고 Jupyter Notebook을 실행하면 커널에 Python만 들어있다.
SageMath를 사용하려면 커널에 등록을 시켜야 하는데 그 방법을 기록해 둔다.


# SageMath 설정

MacOS에서 다음 명령어로 `sage` 를 설치했었다. 현재 내 컴퓨터에 설치된 SageMath 버젼은 8.8이다. ([참고링크](http://macappstore.org/sage/))

```bash
$brew cask install sage
```

그러면 SageMath 앱이 설치되는데 아래 주소에 `kernel.json` 파일을 수정해야 한다.

```plain
/Applications/SageMath-8.8.app/Contents/Resources/sage/local/share/jupyter/kernels/sagemath
```

딕셔너리 형태로 적혀있는데, 다음 항목을 추가하고 저장한다.

```java
"env":{"SAGE_ROOT":"/Applications/SageMath-8.8.app/Contents/Resources/sage"}
```

이걸 안넣으면 Jupyter Notebook에 커널을 추가해도 코드를 만들어서 실행이 되지 않는다. 


# Jupyter Notebook 설정

Anaconda를 실행해서 본인의 Environment의 Terminal을 실행한다. 
수정하지 않았다면 기본 Environment는 base로 되어 있을테니, base 오른쪽 초록 화살표를 클릭해서 Terminal을 실행 할 수 있다. 
Terminal에서 `base` 가 활성화 되어 있는걸 확인하고, 다음 명령어를 실행한다. ([참고링크](https://stackoverflow.com/questions/39296020/how-to-install-sagemath-kernel-in-jupyter))

```bash
$sudo jupyter kernelspec install /Applications/SageMath-8.8.app/Contents/Resources/sage/local/share/jupyter/kernels/sagemath
```

이제 Jupyter Notebook을 실행해보면, 커널에 SageMath 8.8이 추가되어 있는 것을 확인 할 수 있다.


# Comments

별거 아니지만 위 방법을 매번 할 때마다 찾아야 했었다. 피곤..
아마 나중에도 여러번 반복 할 듯하니 기록해 둔다.


<!----- Footnotes ----->

