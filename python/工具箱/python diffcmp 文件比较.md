
* 文本的比较

        text1 = """text1: # 定义字符串 1
        This module provides classes and functions for comparing sequences. including HTML and context and unified diffs.
        difflib document v7.4
        add string
        """
        text1_lines = text1.splitlines() # 以行进行分隔,以便进行对比
        
        text2 = """text2: # 定义字符串 2
        This module provides classes and functions for Comparing sequences. including HTML and context and unified diffs.
        difflib document v7.5"""
        
        text2_lines = text2.splitlines()
        d = difflib.Differ() # 创建 Differ() 对象
        diff = d.compare(text1_lines, text2_lines)
        print '\n'.join(list(diff))

* 文本比较，并以html格式输出

        #encoding=utf-8
        #!/usr/bin/env python
        
        import difflib
        import sys
        
        try:
                textfile1 = sys.argv[1]
                textfile2 = sys.argv[2]
        except Exception , e:
                print "Error:" + str(e)
                print "Usage : diff filename1 , filename2"
                sys.exit()
        
        #定义函数
        def readfile(filename): #文件读取分隔方法
                try:
                        fileHandle = open(filename , 'rb')
                        text = fileHandle.read().splitlines()  #进行行分隔
                        fileHandle.close()
                        return text
                except IOError as error:
                        print("Read file Error:" + str(error))
                        sys.exit()
        
        if textfile1 == "" or textfile2=="":
                print "Usage: filediff: filename1 ,filename2"
                sys.exit()
        
        text1_lines = readfile(textfile1)
        text2_lines = readfile(textfile2)
        
        d = difflib.HtmlDiff()  #创建HtmlDiff 对象
        print d.make_file(text1_lines , text2_lines) #输出html 的对比文件 

* 目录比较
    
    * dircmp 提供了三个输出报告的方法:
    
        report(),比较当前指定目录中的内容;
        report_partial_closure(),比较当前指定目录及第一级子目录中的内容;   
        report_full_closure(),递归比较所有指定目录的内容。 
    
    * 为输出更加详细的比较结果,dircmp 类还提供了以下属性:
    

        left,左目录,如类定义中的 a;
        right,右目录,如类定义中的 b;
        left_list,左目录中的文件及目录列表;
        right_list,右目录中的文件及目录列表;
        common,两边目录共同存在的文件或目录; 
        left_only,只在左目录中的文件或目录;  
        right_only,只在右目录中的文件或目录;  
        common_dirs,两边目录都存在的子目录;  
        common_files,两边目录都存在的子文件;  
        common_funny,两边目录都存在的子目录(不同目录类型或 os.stat() 记录的错误); 
        same_files,匹配相同的文件;
       diff_files,不匹配的文件;
        funny_files,两边目录中都存在,但无法比较的文件;
        subdirs,将 common_dirs 目录名映射到新的 dircmp 对象,格式为字典类型。


* code

        #encoding=utf-8
        #!/usr/bin/env python
        
        import filecmp
        a = "/vagrant/vhost/laravel4"
        b = "/vagrant/vhost/laravel51"
        #进行目录比较，忽略composer.js
        dirObj = filecmp.dircmp(a , b , ['composer.json'])
        
        #进行输出结果比较
        dirObj.report()
        dirObj.report_partial_closure() #比较第一级目录的内容
        dirObj.report_full_closure()   #递归比较所有目录
        
        print "left_list" + str(dirObj.left_list)
        print "right_list" + str(dirObj.right_list)
        print "common:" + str(dirObj.common)
        print "left_only:" + str(dirObj.left_only)
        print "right_only:" + str(dirObj.right_only)
        print "common_dirs:" + str(dirObj.common_dirs)
        print "common_files:" + str(dirObj.common_files)
        print "common_funny:" + str(dirObj.common_funny)
        print "same_file:" + str(dirObj.same_files)
        print "diff_files:" + str(dirObj.diff_files)
        print "funny_files:" + str(dirObj.funny_files)
