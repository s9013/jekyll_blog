---
layout: post
title:  "sublime text"
categories: Tool
---
##1.[sublime text](http://www.sublimetext.com/3)
	

##2.[Install package console](https://packagecontrol.io/installation#st3)

	
	import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

	完事后重启


##3. 安装插件
- Emmet
- JsFormat
- Sublime Prefixr
- ...

##快捷键（shortcut key）



1. Ctr + Shift + L		将选中的多行同时进行编辑
2. Ctrl+J 				将选中的多行代码为一行

待续...


	

	