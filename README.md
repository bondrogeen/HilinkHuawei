![Logo](api/hilink.png)

Клиент для Huawei модемов с прошивками HiLink  

Проверенно на модемах:         
E3372h-153_Update_22.323.01.00.143_M_AT_05.10      
E3372s Update_22.286.53.01.161_S_ADB_TLN_03    
   
Прошивки и другую информацию можно найти тут - http://4pda.ru/forum/index.php?showtopic=582284&    
   

* Установка   
   
$ npm install hilinkhuawei   
   
[![NPM version](http://img.shields.io/npm/v/hilinkhuawei.svg)](https://www.npmjs.com/package/hilinkhuawei)    
[![Downloads](https://img.shields.io/npm/dm/hilinkhuawei.svg)](https://www.npmjs.com/package/hilinkhuawei)    
    
Github: https://github.com/bondrogeen/hilinkhuawei    

* Совместимость
E3372 (МТС 827F/829F, МегаФон M150-2, Билайн E3372/E3370, TELE2 E3372р-153   


	  
* Include  

	var hilink = require('hilinkhuawei');   
	
* Изменить IP адрес (default 192.168.8.1)   

	hilink.setIp('192.168.8.x')   
	
* Изменить отображение статистики трафика  (default - 'auto')   
    
    'auto' - автоматическое отображение в B, KB, MB, GB, TB и времени в 00:00:10    
    'def'  - по умолчанию трафик в битах, время в сек.   
      
    hilink.setTrafficInfo('def')   
    
* Изменить версии модема   (default - '3372s')     

    Прошивки hilink разной версии имеют разную аутентификацию:  
    '3372s' - по token  
    '3372h' - по token и cookie  
    
    hilink.setModel('3372s')   

* Отправка ussd ( *100#, callback )   
   
    hilink.ussd( '*100#', function( response ){  
        console.log(JSON.stringify(response) );  
    });   

* Ответ: *   

	{"response":{   
	"content":["Баланс:88,19р,Лимит:0,01р "],   
	"response":"OK"	}   
	}   

 
* Отправка SMS ( number, text, callback )   
  
	hilink.send( '12345678', 'Hello world', function( response ){   
		console.log( JSON.stringify( response, null, 2 ) );  
	});   
	
* Ответ: *  
  
	{ response: 'OK' }  
	
* Отправка без сохранения  SMS ( number, text, callback )  

	hilink.sendAndDelete( '12345678', 'Hello world', function( sendResponse, deleteResponse ){  
		console.log( JSON.stringify(sendResponse) );  
		console.log( JSON.stringify(deleteResponse) );  
	});
	
* Ответ: *    

	{ response: 'OK' }  
	{ response: 'OK' }  

* Подключиться к сети ('connect',callback)   
* Отключиться от сети ('disconnect',callback)   
* Перезагрузка модема ('reboot',callback)   

hilink.control('conect',function(response ){   
    console.log( JSON.stringify( response, null, 2 ) );   
});

* Ответ: *  

{  response: 'OK'  }  


* Список исходящих сообщений (callback)   

	hilink.listOutbox(function( response ){   
 		console.log( JSON.stringify( response, null, 2 ) );  
	});  
	
* Ответ: *   

   {  
     "response": [   
       {  
         "Smstat": "3",   
         "Index": "40007",   
         "Phone": "123456789",  
         "Content": "4454545454",  
         "Date": "2017-02-25 20:36:30",  
         "Sca": "",   
         "SaveType": "3",  
         "Priority": "4",  
         "SmsType": "1"  
       },  
       {  
         "Smstat": "3",   
         "Index": "40003",  
         "Phone": "123456789",   
         "Content": "121213",  
         "Date": "2017-02-23 14:21:29",   
         "Sca": "",  
         "SaveType": "3",  
         "Priority": "4",  
         "SmsType": "1"  
       }   
     ],  
     "Count": "2"   
   }

    
* Список входящих сообщений (callback)   
  
	hilink.listInbox(function( response ){   
 		console.log( JSON.stringify( response, null, 2 ) );   
	});   
	 
* Ответ: *   

{  
  "response": [  
    {  
      "Smstat": "0",   
      "Index": "40012",  
      "Phone": "+123456789",  
      "Content": "test",   
      "Date": "2017-02-25 21:04:45",  
      "Sca": "",  
      "SaveType": "4",  
      "Priority": "0",  
      "SmsType": "1"   
    },  
    {   
      "Smstat": "1",  
      "Index": "40001",   
      "Phone": "Balance",   
      "Content": "Баланс:62,39р,Лимит:0,01р",  
      "Date": "2017-02-23 14:20:52",   
      "Sca": "",  
      "SaveType": "4",   
      "Priority": "0",   
      "SmsType": "2" 
    }  
  ],  
  "Count": "2"  
}  
    
 
    
Список только новых входящих сообщений (callback)      
    
    hilink.listNew(function(response ){   
        console.log( JSON.stringify( response, null, 2 ) );  
    });   


* Ответ: *      
    
{  
  "response": [  
    {  
      "Smstat": "0",   
      "Index": "40010",   
      "Phone": "+123456789",   
      "Content": "test text",    
      "Date": "2017-02-25 20:37:53",  
      "Sca": "",    
      "SaveType": "4",  
      "Priority": "0",  
      "SmsType": "1"  
    },  
    {  
      "Smstat": "0",   
      "Index": "40009",   
      "Phone": "+123456789",   
      "Content": "test text",  
      "Date": "2017-02-25 20:37:50",  
      "Sca": "",  
      "SaveType": "4",  
      "Priority": "0",  
      "SmsType": "1"  
    },  
    {  
      "Smstat": "0",  
      "Index": "40008",  
      "Phone": "+123456789",  
      "Content": "test new sms",  
      "Date": "2017-02-25 20:37:47",   
      "Sca": "",   
      "SaveType": "4",   
      "Priority": "0", 
      "SmsType": "1"   
    }
  ],
  "Count": 3
}
    
* Пометить как прочитаное сообщение   (index,callback)  
    
    hilink.setRead('40001',function(response ){  
        console.log( JSON.stringify( response, null, 2 ) );  
    });  
    
* Ответ: *  
 
 {  response: 'OK'  }  
 
* Пометить все сообщения как прочитаные  

    hilink.readAll(function(response ){  
        console.log( JSON.stringify( response, null, 2 ) );  
    });
 
* Ответ: *   
  
{  
  "response": [  
    "40022",   
    "40006",  
    "40004"   
  ], 
  "Count": 3   
}   
   
    
* Очистка входящих сообщений  

	hilink.clearInbox();  
	  
* Очистка исходящих сообщений    

	hilink.clearOutbox();    
  
* Удаление сообщения по индексу    

    hilink.delete( '40007', function( response ){    
        console.log(JSON.stringify(response) );    
    });   

* Ответ: *  

{  response: 'OK'  }   
  

* Статус (callback)   
  
	hilink.status(function( response ){   
        console.log( JSON.stringify( response, null, 2 ) );   
    });       
   
* Ответ: *    
     
	{   
      "response": {   
        "ConnectionStatus": "CONNECTED",   
        "SignalIcon": "3",   
        "CurrentNetworkType": "LTE",    
        "CurrentServiceDomain": "3",   
        "RoamingStatus": "0",    
        "simlockStatus": "0",    
        "WanIPAddress": "123.123.123.123",   
        "PrimaryDns": "11.11.24.4",   
        "SecondaryDns": "11.11.114.15",      
        "currenttotalwifiuser": "0",  
        "ServiceStatus": "2",   
        "SimStatus": "1",   
        "CurrentNetworkTypeEx": "101",   
        "maxsignal": "5",    
        "wifiindooronly": "-1",  
        "wififrequence": "0",    
        "classify": "hilink",    
        "flymode": "0"    
      }    
    }     



* Уведомление (callback)    
    
    	hilink.notifications(function( response ){   
            console.log( JSON.stringify( response, null, 2 ) );    
        });      
    
* Ответ: *    
   
{     
  "response": {     
    "UnreadMessage": "0",    
    "SmsStorageFull": "0",   
    "OnlineUpdateStatus": "10"    
  }     
}    

* Статус оператора сети (callback)    

    	hilink.statusNet(function( response ){    
            console.log( JSON.stringify( response, null, 2 ) );   
        });   

* Ответ: *    

{   
  "response": {   
    "State": "0",    
    "FullName": "MTS-RUS",   
    "ShortName": "MTS",    
    "Numeric": "25001",   
    "Rat": "7"   
  }   
}   

* Состояние о кол. смс (callback)   

    	hilink.smsCount(function( response ){   
            console.log( JSON.stringify( response, null, 2 ) );   
        });   

* Ответ: *   
   
{   
  "response": {    
    "LocalUnread": "0",   
    "LocalInbox": "3",    
    "LocalOutbox": "1",   
    "LocalDraft": "2",   
    "LocalDeleted": "0",   
    "SimUnread": "0",      
    "SimInbox": "1",   
    "SimOutbox": "0",   
    "SimDraft": "0",   
    "LocalMax": "500",   
    "SimMax": "5",   
    "SimUsed": "1",    
    "NewMsg": "0"   
  }   
}   
   
* Уровень сигнала (callback)   
  
    	hilink.signal(function( response ){   
            console.log( JSON.stringify( response, null, 2 ) );   
        });   

* Ответ: *   

{   
  "response": {    
    "pci": "123",   
    "cell_id": "123456789",   
    "rsrq": "-7dB",    
    "rsrp": "-97dBm",   
    "rssi": "-81dBm",   
    "sinr": "8dB",   
    "mode": "7"   
  }   
}   
   
* Адреса  (callback)   

    	hilink.settingsNet(function( response ){    
            console.log( JSON.stringify( response, null, 2 ) );    
        });   

* Ответ: *   

{  
  "response": {   
    "DhcpIPAddress": "192.168.8.1",   
    "DhcpLanNetmask": "255.255.255.0",   
    "DhcpStatus": "1",    
    "DhcpStartIPAddress": "192.168.8.100",   
    "DhcpEndIPAddress": "192.168.8.200",   
    "DhcpLeaseTime": "86400",   
    "DnsStatus": "1",   
    "PrimaryDns": "192.168.8.1",   
    "SecondaryDns": "192.168.8.1"    
  }   
}   

* Информация о модеме (callback)   

    	hilink.basicInfo(function( response ){
            console.log( JSON.stringify( response, null, 2 ) );
        });

* Ответ: *    

{   
  "response": {    
    "productfamily": "LTE",    
    "classify": "hilink",   
    "multimode": "0"   
  }   
}   

* Статистика трафика (callback)

    	hilink.traffic(function( response ){
            console.log( JSON.stringify( response, null, 2 ) );
        });

* Ответ: *

{
  "response": {
    "CurrentConnectTime": "00:25:46",   
    "CurrentUpload": "1.41 MB",   
    "CurrentDownload": "75.87 MB",   
    "CurrentDownloadRate": "5.35 KB",   
    "CurrentUploadRate": "717 B",   
    "TotalUpload": "455.63 MB",   
    "TotalDownload": "14.66 GB",   
    "TotalConnectTime": "94:34:16",   
    "showtraffic": "1"   
  }
}

* Статистика трафика за месяц (callback)   


    	hilink.trafficMonth (function( response ) {
            console.log( JSON.stringify( response) );
        });


* Ответ: *

{
  "response": {
    "CurrentMonthDownload": "14.67 GB",   
    "CurrentMonthUpload": "455.74 MB",   
    "MonthDuration": "94:35:40",   
    "MonthLastClearTime": "2017-2-21"   
  }
}


   Changelog 
      
   2.1.3   
   
fix ussd  
     
   2.1.1   
   
Добавил 3372H   
   
   2.0.0    
   
Изменил ответ    
   
   1.1.1    
   
Добавил новые функции    
   
   1.0.0    
   
Изменения запросов пакету     
   
   0.2.1    
   
Добавил  статистику трафика за месяц, изменил отображение статистики трафика, статус подключения и отображения типа сети. 
Добавил ответ от оператора от USSD запроса. 
Удаление по индексу сообщения.
			
			
   0.1.2 
   
   Добавил ussd команды
   
   0.1.1 

    
