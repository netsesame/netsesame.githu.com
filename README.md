netsesame.githu.com
===================

import web.rest.client;
import string.html;

class qqRobot {

    ctor(){
        var client = ..web.rest.client(); 
         
        var loginUrl = ..string.match(
            client.request( "http://pt.3g.qq.com/" ) 
            ,"(<@http://pt.3g.qq.com/handleLogin?vdata=@>.+?)\""" 
        );
        
        client.declareApi( loginUrl,"login","POST" )
    } 

    login = function(qq, pwd) {  
        if(!qq)error("请指定QQ号码",2);
        
        var data  = client.login( 
            login_url = "http://pt.3g.qq.com/s?aid=nLogin";
            sidtype = 1;
            loginTitle = "手机腾讯网";
            bid = 0;
            qq = qq;
            pwd = pwd;
            loginType = 1;
        )
          
        if( ..string.find(data,"验证码" )  ){
             var scode = ..string.match(data,"\<img src=\""(.+?)\""" ); 
             return null,"需要输入验证码",scode;
        }
        var sid = ..string.match(data,"sid=(.+?)\&" ); 
        
        if( sid ){
            client.declareApi( "http://q16.3g.qq.com/g/s?sid=" + sid,"sendMsg" )
            client.declareApi( "http://q16.3g.qq.com/g/s?sid=" + sid + "&3G_UIN=" + qq + "&saveURL=0&aid=nqqChat","getMsg" )
            client.declareApi( "http://pt.3g.qq.com/s?sid=" + sid + "&aid=nLogout","logout","GET" )
            return true;
        }
    }

    sendMsg = function(toQq, msg ) {
    
        if ( client.sendMsg ){
            return client.sendMsg (
                ["msg"] =  msg;
                ["u"] =  toQq;
                ["saveURL"] =  0; 
                ["on"] =  1;
                ["aid"] =  "发送";
                ["do"] =  "send";
            ) 
        } 
    }

    getMsg = function() {
    
        if ( client.getMsg ){
            var data = client.getMsg();  
            data = ..string.match(data,"发送短信给他(.+)聊天记录查看") 
            return data ? ..string.html.toText(data)
        }
    }
    
    logout = function(){
        if (client.logout) 
            client.logout(); 
    }
}


//创建QQ客户端
var robot = qqRobot();

//登录QQ
robot.login( 我的QQ,"登录密码" )

//发送信息
robot.sendMsg( 好友QQ,"发送测试信息" )
  
