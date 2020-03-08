# jsNiXiang_weibo
python-使用js逆向方法登陆微博

def main():
    #第一步：登陆前期准备，把账号密码传入js逆向函数，获得登陆时需要的参数me,su,sp
    su = get_su()
    me = get_me(su)
    sp = get_sp(pwd,me)
    #第二步：把参数me,su,sp传入login()登陆请求函数，将获得正在登陆页面，如果第二步登陆成功，将获得转跳链接location_url
    location_url=login(me,su,sp)
    #第三步：发送location_url转跳链接请求，如果转跳成功，返回页面信息。
    #解码location_parse页面信息，获得参数ssosavestate,ticket，为第四步登陆作准备
    response=location(location_url)
    ssosavestate,ticket=location_parse(response)
    #第四步：把第三步返回的参数传入ticket_login，发送ticket_login请求，如果网页信息显示result=True,则登陆成功，下一步便可以登陆自己的主页啦。
    ticket_login(ssosavestate,ticket)
    my_url='https://weibo.com/u/3607627654/home?wvr=5&lf=reg'
    my_login(my_url)
    
     #难点总结:首先需要找到登陆时需要的参数me,su,sp,可以使用js逆向函数把账号输入而获得登陆参数。
    #1、在查找js代码时，可以打断点抓包，也可以输入错误的密码转包(因为错误的密码也能使页面停在转跳的地方)
    #2、复写js代码时，注意/转译，因为/在python属于特殊字符，使用//变为普通字符
    #3、ctrl+f可以在chrome的sources下搜索
    #4、浏览器开发工具的console可以调试js代码，使用shift+enter进行换行，enter执行代码，console.log()输出结果
    #5、跨域时可能会找不到跳转之前的js代码
