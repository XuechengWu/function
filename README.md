# 自制函数
```
mycopyfile(需要复制移动的文件, 目的地址)

zipDir(目标文件夹路径, 压缩文件保存路径+xxxx.zip)

copy_allfiles(原文件夹, 目标文件夹)

delete_space(目标所在的文件夹)

os.remove(path)   #删除文件

os.removedirs(path)   #删除空文件夹

shutil.rmtree(path)    #递归删除文件夹
```

```
import os
import shutil
import zipfile

# srcfile 需要复制、移动的文件   
# dstpath 目的地址
 
def mycopyfile(srcfile,dstpath):                       # 复制函数
    if not os.path.isfile(srcfile):
        print ("%s not exist!"%(srcfile))
    else:
        fpath,fname=os.path.split(srcfile)             # 分离文件名和路径
        if not os.path.exists(dstpath):
            os.makedirs(dstpath)                       # 创建路径
        shutil.copy(srcfile, dstpath + fname)          # 复制文件
        print ("copy %s -> %s"%(srcfile, dstpath + fname))
 
 
# src_dir = './'

def zipDir(dirpath, outFullName):
    """
    压缩指定文件夹
    :param dirpath: 目标文件夹路径
    :param outFullName: 压缩文件保存路径+xxxx.zip
    :return: 无
    """
    zip = zipfile.ZipFile(outFullName, "w", zipfile.ZIP_DEFLATED)
    for path, dirnames, filenames in os.walk(dirpath):
        # 去掉目标跟路径，只对目标文件夹下边的文件及文件夹进行压缩
        fpath = path.replace(dirpath, '')
 
        for filename in filenames:
            zip.write(os.path.join(path, filename), os.path.join(fpath, filename))
    zip.close()
    
    
def copy_allfiles(src,dest):
#src:原文件夹；dest:目标文件夹
  src_files = os.listdir(src)
  for file_name in src_files:
    full_file_name = os.path.join(src, file_name)
    if os.path.isfile(full_file_name):
        shutil.copy(full_file_name, dest)

def delete_space(buff_dir):
#buff_dir:目标所在的文件夹
    for files_name in os.listdir(buff_dir):
        if len(files_name.split(" ")) >1:
            os.rename(os.path.join(buff_dir,files_name),
                      os.path.join(buff_dir,files_name.replace(" ","_")))
            print(os.path.join(buff_dir,files_name.replace(" ","_")))

```
