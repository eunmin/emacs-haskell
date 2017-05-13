# Haskell Emacs 설정하기

Haskell 개발하기 위해 Emacs 설정하는 과정을 기록으로 남긴다.
문서는 [여기](https://github.com/serras/emacs-haskell-tutorial/blob/master/tutorial.md)를
참고 했다. Emacs 버전은 macOS 25.1.1 버전이고 GUI 버전이 아니고 그냥 터미널 버전을 쓰고 있다.
Emacs 패키지 관리는 `use-package`를 사용하고 있다. Haskell 라이브러리는 `stack`으로 관리한다.

## haskell-mode 설정하기

`init.el`에 아래와 같이 `haskell-mode` 패키지를 사용한다고 설정한다.

```elisp
(use-package haskell-mode
  :ensure t)
```

Emacs를 실행하면 `haskell-mode`가 설치된다. 만약 설치가 안되면 `package-refresh-contents`로
최신 패키지 목록으로 업데이트 한 후에 다시 실행해보자.

`.hs` 파일을 열어보면 Emacs 하단에 `Haskell` 표시가 되고 문법 하이라이팅이 잘 되는 것을 볼 수 있다.

## hindent 적용하기

Haskell 포맷팅 도구인 hindnet를 Emacs에 적용하면 편리하다. hindent는 `stack`으로 설치한다.
문서에 나온 것처럼 `happy`도 설치하라고 하니 그냥 설치한다. hindent에 대한 자세한 내용은
[여기](https://github.com/commercialhaskell/hindent)를 참고한다.

```bash
stack update
stack install happy
stack install hindent
```

Emacs에 연동해서 사용하기 위해서 `use-package`로 `hindent` 패키지를 설치한다.
그리고 `haskell-mode`에서 사용하기 위해 `haskell-mode` hook에 `hindent`를 설정한다.

```elisp
(use-package hindent
  :ensure t)

(use-package haskell-mode
  :ensure t
  :config
  (add-hook 'haskell-mode-hook #'hindent-mode))
```

Emacs를 실행하고 `.hs` 파일을 아무거나 열어서 `M-q`를 누르면 커서가 있는 구문을 포맷팅 해준다.
블럭을 지정하고 `C-M-\`를 하면 블럭에 있느 코드를 포맷팅 해준다.
