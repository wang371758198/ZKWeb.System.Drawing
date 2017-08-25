# System.Drawing for .NET Core, that really work

This is a .Net Core compatible System.Drawing implementation modified from mono project.<br/>
Works on windows and linux.

Since 3.0, namespace is replaced to `System.DrawingCore`, please modify your code after upgrade.
Since 4.0, netstandard 2.0 is required, and code is updated to mono 5.2.0.215.

[![NuGet](https://buildstats.info/nuget/ZKWeb.System.Drawing)](http://www.nuget.org/packages/ZKWeb.System.Drawing)

These system are tested:

- Windows 8.1 64bit
- Ubuntu Server 16.04 LTS 64bit
- Fedora 24 64bit
- CentOS 7.2 64bit

These features should work:

- Open jpg, bmp, ico, png
- Save jpg, bmp, ico, png 
- Resize image
- Draw graphics with brush and pen
- Open font and draw string

Known issues:

- #1 Save icon file large than 255x255 will cause arithmetic overflow error

# Warning

Microsoft will ship their [System.Drawing](https://github.com/dotnet/corefx/tree/master/src/System.Drawing.Common) soon,<br/>
it's also modified from mono and I believe it's more stable than mine,<br/>
so this project may discontinue soon after offical System.Drawing available.<br/>

# How can I get it work?

On windows, just install package `ZKWeb.System.Drawing` from nuget.

On Linux, except install package `ZKWeb.System.Drawing` from nuget, you need install `libgdiplus`.<br/>

- Ubuntu 16.04 and above:
	- apt-get install libgdiplus
	- cd /usr/lib
	- ln -s libgdiplus.so gdiplus.dll
- Fedora 23 and above:
	- dnf install libgdiplus
	- cd /usr/lib64/
	- ln -s libgdiplus.so.0 gdiplus.dll
- CentOS 7 and above:
	- yum install autoconf automake libtool
	- yum install freetype-devel fontconfig libXft-devel
	- yum install libjpeg-turbo-devel libpng-devel giflib-devel libtiff-devel libexif-devel
	- yum install glib2-devel cairo-devel
	- git clone https://github.com/mono/libgdiplus
	- cd libgdiplus
	- ./autogen.sh
	- make
	- make install
	- cd /usr/lib64/
	- ln -s /usr/local/lib/libgdiplus.so gdiplus.dll

**Then you should replace all `System.Drawing` To `System.DrawingCore` in your code**

# Huh? What's the different with CoreCompat.System.Drawing?

- No fake strong name is used, will not mess up Asp.Net and OWIN.
- Copied all files from mono 5.2.0.215, you will actually compile it without seeing hundreds error
- Really tested on linux and really work
- You can actually run tests from `dotnet test`, no joke
	- Windows
		- .Net Core: Test Count: 1856, Passed: 1480, Failed: 367, Warnings: 0, Inconclusive: 0, Skipped: 9
		- .Net Framework: Test Count: 1856, Passed: 1479, Failed: 368, Warnings: 0, Inconclusive: 0, Skipped: 9
	- Linux
		- .Net Core: TODO
- No reference to System.Drawing.Primitive, because System.Drawing.Primitive reference original System.Drawing on .Net Framework which may cause conficts error
- Namespace is renamed from `System.Drawing` to `System.DrawingCore` because vs2017's new project system is so stupid

# Mac support

Not tested yet.
