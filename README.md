# 将.pvr.ccz批量转换为png格式
# Author:www.coolketang.com
# Date: 2019-03-28

# pvr.ccz图片所在的文件夹
path="/Users/jerry/Desktop/coolketang/pvr"
# TexturePacker软件的文件，需要在Applications找到TexturePacker，然后点击右键，选择显示包内容，接着找到TexturePacker
TexturePacker="/Applications/TexturePacker.app/Contents/MacOS/TexturePacker"
# 文件格式
fileType="*.pvr.ccz"

# 搜索命令
allFiles=`find $path -name $fileType`

# 搜索得到的数组循环处理
for i in $allFiles;
	do
		# 把文件后缀名删除
		fileName=${i%%.*};
		# 执行TexturePacker命令，转换文件的格式。在此不生成plist文件，使用原来的plist文件。注意此处设置padding为0，默认值为2，您可以根据具体情况设置它的值，否则可能在取图时位置有所偏差。
		$TexturePacker $i --sheet ${fileName}".png" --format cocos2d --padding 0 --opt RGBA8888 --allow-free-size --algorithm MaxRects --no-trim --dither-none-nn;
		# 删除原来的pvr.ccz文件。
		rm ${fileName}".pvr.ccz";
	done

echo "Mission completed."
