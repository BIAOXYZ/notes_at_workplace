
# 官方

os --- 多种操作系统接口 https://docs.python.org/zh-cn/3/library/os.html || os — Miscellaneous operating system interfaces https://docs.python.org/3/library/os.html

# 其他

Python OS 文件/目录方法 https://www.runoob.com/python/os-file-methods.html

How do I get the full path of the current file's directory? https://stackoverflow.com/questions/3430372/how-do-i-get-the-full-path-of-the-current-files-directory
- https://stackoverflow.com/questions/3430372/how-do-i-get-the-full-path-of-the-current-files-directory/3430395#3430395
  ```py
  import os
  os.path.abspath(os.getcwd())
  ```

How to set the current working directory? [duplicate] https://stackoverflow.com/questions/1810743/how-to-set-the-current-working-directory/1810760
- https://stackoverflow.com/questions/1810743/how-to-set-the-current-working-directory/34971949#34971949
  * > To set the working directory:
    ```py
    import os
    print os.getcwd()  # Prints the current working directory
    os.chdir('c:\\Users\\uname\\desktop\\python')  # Provide the new path here
    ```
    >> //notes：其实一般合成一句 `os.chdir(os.getcwd())` 就可以了。
