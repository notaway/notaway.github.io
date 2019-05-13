---
layout:    post
title:     本文为文才学院课程自动学习辅助程序思路
date:      2019-5-13 20:18:18
summary:  自动化程序
categories: Program
tags: Python
excerpt: 记录如何提升学习工作效率，节省时间锻炼身体
mathjax: true
---

### 文才学院课程自动学习

#### 环境搭建

    可以参考这篇文章 
    需要安装的：

    安装python
    安装pip
    安装 selenium 
    安装 chromedriver(firefox对应的也可以)


#### 程序思路：

    其实思路很简单就是模拟手动操作，这样思路简单，也可以有效防止网站检测机器人。


首先模拟登陆：
    
    代码如下：

        def login(self):
            self.browser.get('http://crjy.wencaischool.com/hngc/console/')
            loginBtn = self.wait.until(EC.element_to_be_clickable((By.CLASS_NAME, 'loginBtn')))
            loginBtn.click()
            time.sleep(1)
            username_input = self.until(EC.presence_of_element_located((By.ID, 'userName')))
            self.input_text(username_input, self.username)
            password_input = self.until(EC.presence_of_element_located((By.ID, 'userPwd')))
            self.input_text(password_input, self.password)
            login_button = self.wait.until(EC.element_to_be_clickable((By.ID, 'submitBtn')))
            time.sleep(2)
            login_button.click()


再次时课程学习：

        首先访问学习界面：

        self.browser.get("http://crjy.wencaischool.com/hngc_student/console/apply/studyOnline/index.html")
        time.sleep(1)
        ke_cheng = self.browser.find_elements_by_class_name('dospan')
        ke_cheng[2].click()
        time.sleep(10)
        self.browser.switch_to.window(self.browser.window_handles[-1])
        print(self.browser.window_handles)
        print(self.browser.current_window_handle)
        self.browser.switch_to.frame('w_main')

    再次模拟点击，打开需要学习的子课程，这里遇到问题，由于对javascript不太了解，所以没有再selenium中嵌入javascript代码，直接打开相关课程，

    进入到学习界面后，一直返回无法找到课程列表，查看网页源代码发现，课程列表实在另外的iframe下，需要选中相应的iframe。

    代码如下：
        self.browser.switch_to.frame('w_main')
        xuexi_link = self.browser.find_elements_by_class_name('childSection')
    for element in xuexi_link[1:100:1]: # 这里没有直接判断课程长度，默认为100
        try:
            self.browser.execute_script("arguments[0].scrollIntoView();", element) #在selenium 中执行javascript程序。
            element.click()
            time.sleep(random.randrange(100, 130))  #随机停留100~130s
        except Exception as e:
                print(e)
                self.browser.close()  #出错关闭浏览器





