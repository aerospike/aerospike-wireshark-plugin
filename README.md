README
======

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

This plugin is implemented using the Lua
programming language. The Wireshark version that you use needs to have
built-in support for Lua. You can check the same in Wireshark by
clicking on the menu *Help* -> *About Wireshark*, and you should see a
string *with Lua <version>*.

The plugin has been tested on Wireshark version 2.2.6 with Lua 5.2.4
on Ubuntu and Mac OS X operating systems.

Warning
=======

This project is still highly experimental and subject to breaking
changes. Use it at your own risk.

Usage
=====

You can start the Lua plugin with your Wireshark packet capture file
as shown below:

    $ wireshark -X lua_script:aerospike.lua file-capture.pcapng

Configuration
=============

You need to ensure that Lua support is not disabled in
/etc/wireshark/init.lua:

    disable_lua = false

If you would like the plugin to be loaded on startup, you can place
the plugin in *~/.wireshark/plugins* folder. You might also want to
refer the "Plugin folders" section in the user guide:

  https://www.wireshark.org/docs/wsug_html_chunked/ChPluginFolders.html

Plugin
======

The Aerospike Wireshark Lua plugin is at *lua/aerospike.lua*.

You can also generate the aerospike.lua file using the following command:

    $ less -f "docs/aerospike.lua.md" | lit2lua > lua/aerospike.lua

You can use luarocks to install lualit. The version of luarocks used
is 2.2.0, and that of lualit used during development is 0.0.2-1.

Docs
====

Literate programming has been used to inline documentation with code
in a Markdown format. The same is available at *docs/aerospike.lua.md*.

Protocols
=========

The following Aerospike wire protocols are supported:

| Protocol  | 
|----------:|
| Info      |
| Message   |
| Heartbeat |
| Batch     |

Testing
=======

You can run automated tests using the following commands from the
tests/ folder:

    $ cd tests
    $ make clean && make test

Coverage
========

luacov and luacov-console installed using luarocks are required to
produce code coverage report. Running the tests will also generate the
coverage summary report.

When using Wireshark version prior to 2.6.4, the following additional
changes need to be done:

1. Update /usr/local/share/lua/5.1/luacov/hook.lua (or
   ~/.luarocks/share/lua/5.1/luacov/hook.lua) with:

    - local name = debug.getinfo(level, "S").source
    + local name = "@../lua/aerospike.lua"

2. If installing Luarocks packages to /usr, you need to give access to non-root user:

    $ cd /usr/local/share/lua/5.1
    $ sudo chmod a+r *

Source: https://github.com/keplerproject/luacov/issues/55
        https://github.com/luarocks/luarocks/wiki/Using-LuaRocks

Bugs
====

Please file GitHub issues if you find any bugs or have feature requests.

References
==========

1. Wireshark with Lua support. https://wiki.wireshark.org/Lua#Getting_Started

2. Luarocks. https://luarocks.org/
