# Commons


```emacs-lisp
(let ((bootstrap-file
       (expand-file-name "straight/repos/straight.el/bootstrap.el" user-emacs-directory))
      (bootstrap-version 5))
  (unless (file-exists-p bootstrap-file)
    (with-current-buffer
        (url-retrieve-synchronously
         "https://ghproxy.com/https://raw.githubusercontent.com/sangjeedondrub/commons/main/install.el"
         'silent 'inhibit-cookies)
      (goto-char (point-max))
      (eval-print-last-sexp)))
  (load bootstrap-file nil 'nomessage))
```

```emacs-lisp
;; Faster `straight' by using Github mirror in mainland China
(defun sangjee/set-github-mirror (oldfunc &rest args)
  (let ((url (apply oldfunc args)))
    (replace-regexp-in-string (rx (group "https://github.com"))
                              "https://ghproxy.com/https://github.com" url nil nil 1)))
(advice-add 'straight-vc-git--encode-url :around #'sangjee/set-github-mirror)
```