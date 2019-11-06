---
title: Docker メモ
date: 2019-11-05 18:31:19
tags: ['docker', 'container', 'development']
---

## Dockerfile

### キーワード

#### FROM
　FROMは作成するDockerイメージのベースとなるイメージを指定でいる。
　FROMで指定できるDockerイメージはDocker Hubに公開されているものから指定できる。

#### LABEL
　イメージ作者の情報などを記述。

### ENV
　Dockerコンテナ内で使える環境変数を設定できる。

### ARG
　ビルド時に指定する引数から値を受け取ることができる。
　Dockerfile内で指定したARGの引数と、ビルド時に指定する引数はそろえる必要がある。

```
#コマンド：sampleargがそろえるべき名前
> docker image build --build-arg samplearg=okok -t example/dockerimage .

#Dockerfileでは以下のように名前を指定して二行目のように値を取り出すことができる。
ARG samplearg
ENV BUILD_ARG=${samplearg}
```



#### RUN
　RUNはDockerイメージビルド時に、Dockerコンテナ内で実行するコマンドを定義する。
　RUNの引数には実行したいコマンドをそのまま記述する。

#### COPY
　COPYはDockerを動作させているホストマシン上のファイルやディレクトリをDockerコンテナ内にコピーするためのキーワード。

#### CMD
　CMDはDockerコンテナとして実行する際に、コンテナ内で実行するプロセスを指定する。
　RUNはイメージをビルドするために使い、CMDはコンテナ起動時に一度実行される。

#### ENTRYPOINT
　ENTRYPOINTにはコマンドを記述する。CMDはENTRYPOINTへの引数となる。--entrypointでrun時に指定することで上書きできる。

## ビルド

```
docker image build -t イメージ[:タグ名] Dockerfileまでのパス
```

タグ名は省略するとlatestとなる。

## イメージからコンテナの実行

```
docker container run イメージ名[/追加のパス]:タグ名
```

