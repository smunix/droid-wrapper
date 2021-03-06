概要
====

Android 向けにネイティブプログラムをコンパイルしようとすると、
コンパイル時やリンク時にフラグを山ほどつける必要がある。

さらに、共有ライブラリのリンク時とプログラムのリンク時の
オプションが異っていたりするので、autotools 系 (autoconf,
automake, libtoolなど）を使っているプログラムのポーティングが
困難である。

そこで、これらを解決するために gcc や ld に対するラッパを作成した。
このラッパを利用すれば、コンパイル/リンク時のオプションが自動的に
付加される。


インストール
============

    $ sudo make install

droid-gcc, droid-g++, droid-ld の３つのコマンドがインストール
される。


使い方
======

以下の環境変数を設定する

 *  DROID_ROOT : Android ソースツリーディレクトリ
 *  DROID_TARGET : コンパイルターゲット (generic や dream-open など)
 *  DROID_HOST : ビルドホストを指定。
    Windows では "windows", Mac OS X では "darwin-x86"
    に指定 (Linux の場合は指定不要)
 *  DROID_WRAPPER_DEBUG : デバッグ時に適当な値に設定

あとはそのまま droid-gcc, droid-ld などを使う。

    例)
    $ droid-gcc -O2 -c foo.c
    $ droid-ld -o foo foo.o

configure を使っているソフトウェアをコンパイルする場合は、以下のよう
にする。

    $ CC=droid-gcc LD=droid-ld ./configure --host=arm-none-linux-gnueabi


agcc との違い
=============

本ラッパは http://plausible.org/andy/agcc に触発されて作成した。
やっていることは同じようなものだが、以下の点が異なる。

 *  本スクリプトでは、コマンドラインは本来のツールにすべて引き渡される。
    これは configure スクリプトを使うようなソフトウェアでは重要である。
 *  本スクリプトは、g++, ld にも対応している。

----
村上 卓弥 <tmurakam at tmurakam.org>
