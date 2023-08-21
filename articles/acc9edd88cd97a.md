---
title: "【Git】fast-forwardについて"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Github"]
published: true
---

## fast-forwardとは？
fast-forward = 早送りの意味


**あるAブランチ**と**Bブランチ**を比較した際に、前者(A)が後者(B)をcommitとして含まれている(進んでいる)形となっている事


```git
git log remotes/origin/otoro
commit 80c803c810eab02295e29f573a3705c4787b78cd (origin/otoro)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Mon Apr 11 23:26:35 2022 +0900

    add another html

commit 9e4f4ec75d266ab405339d3ef98b1fb65dc0968d (origin/oyster)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:49:43 2022 +0900

    add oyster log

commit dd69904112592fb0f25f90050ec3621462b5448c (origin/squid)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:27:19 2022 +0900

    chagne console log with squid

commit eb590a7fce738f3c0263546ef63b40dae717550f
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:17:05 2022 +0900

    change console log output to sushi emoji

commit cb5552f23eac554c3eb3723b6aa38b857a2f470f (origin/maguro)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:10:07 2022 +0900

    add JavaScript Playground from https://github.com/DiveIntoHacking/one-liners

commit e09921bba1db763543adebc1b1e7f0b5d9511c6e (origin/init)
Author: Atsushi Ishida <gipcompany@users.noreply.github.com>
Date:   Fri Apr 8 21:46:21 2022 +0900

    Initial commit

```
上記でも確認できるが、**git checkout -t origin/maguro**を行った後にorotoとの差分を確認する

```git
git-sushi on  maguro 🤖 v16.20.0
❯
git diff maguro..origin/otoro
diff --git a/javascript.js b/javascript.js
index 950e532..cd85a65 100644
--- a/javascript.js
+++ b/javascript.js
@@ -1 +1,2 @@
-console.log('Hello, JavaScript!');
+console.log('Hello, 🦑!');
+console.log('Hello, 🦪!');
diff --git a/public/index.html b/public/index.html
new file mode 100644
index 0000000..e611add
--- /dev/null
+++ b/public/index.html
@@ -0,0 +1,13 @@
+<!DOCTYPE html>
+<html lang="ja">
+  <head>
+    <meta charset="UTF-8" />
+    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
+    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
+    <title>I am otoro.</title>
+  </head>
+
+  <body>
+    I am otoro.
+  </body>
+</html>


```

```git
git-sushi on  maguro 🤖 v16.20.0
❯
git merge origin/otoro
Updating cb5552f..80c803c
Fast-forward
 javascript.js     |  3 ++-
 public/index.html | 13 +++++++++++++
 2 files changed, 15 insertions(+), 1 deletion(-)
 create mode 100644 public/index.html
```
ここで**git merge origin/otoro**としたが、**git merge --ff origin/otoro**のオプションが省略されている
```git
git log
commit 80c803c810eab02295e29f573a3705c4787b78cd (HEAD -> maguro, origin/otoro)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Mon Apr 11 23:26:35 2022 +0900

    add another html

commit 9e4f4ec75d266ab405339d3ef98b1fb65dc0968d (origin/oyster)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:49:43 2022 +0900

    add oyster log

commit dd69904112592fb0f25f90050ec3621462b5448c (origin/squid)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:27:19 2022 +0900

    chagne console log with squid

commit eb590a7fce738f3c0263546ef63b40dae717550f
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:17:05 2022 +0900

    change console log output to sushi emoji

commit cb5552f23eac554c3eb3723b6aa38b857a2f470f (origin/maguro)
Author: Atsushi Ishida <gipcompany@gmail.com>
Date:   Fri Apr 8 22:10:07 2022 +0900

    add JavaScript Playground from https://github.com/DiveIntoHacking/one-liners

commit e09921bba1db763543adebc1b1e7f0b5d9511c6e (origin/init)
Author: Atsushi Ishida <gipcompany@users.noreply.github.com>
Date:   Fri Apr 8 21:46:21 2022 +0900

    Initial commit

```

