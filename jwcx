def jwcx(xh,mima,sou,xunh):
    import requests
    from bs4 import BeautifulSoup
    import re
    import base64
    import json
    s= requests.Session()
    url1='http://inquiry.ecust.edu.cn/jsxsd/'
    a=s.get(url1)
    c1=a.headers['Set-Cookie']
    co=re.split(';',c1)[0]
    header={
   'Accept': 'image/png, image/svg+xml, image/*; q=0.8, */*; q=0.5',
   'Accept-Encoding': 'gzip, deflate',
   'Accept-Language': 'zh-CN',
   'Connection': 'Keep-Alive',
   'Cookie': co,
   'Host': 'inquiry.ecust.edu.cn',
   'Referer': 'http://inquiry.ecust.edu.cn/jsxsd/',
   'Upgrade-Insecure-Requests': '1',
   'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134'}
    c=s.post('http://inquiry.ecust.edu.cn/jsxsd/verifycode.servlet',headers=header)
    urlocr = "https://aip.baidubce.com/rest/2.0/ocr/v1/general_basic";
    token="24.de4674535a6a6e3a3974e36051b8cba6.2592000.1533009979.282335-10966803";
    application="application/x-www-form-urlencoded";
    ocr = requests.post(urlocr, data={"access_token": token,"image":base64.b64encode(c.content),"Content-Type":application})
    yzm=json.loads(ocr.text)['words_result'][0]['words']
    import execjs
    jm=execjs.compile('''
var keyStr = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
function encodeInp(input) {
    var output = "";
    var chr1, chr2, chr3 = "";
    var enc1, enc2, enc3, enc4 = "";
    var i = 0;
    do {
        chr1 = input.charCodeAt(i++);
        chr2 = input.charCodeAt(i++);
        chr3 = input.charCodeAt(i++);
        enc1 = chr1 >> 2;
        enc2 = ((chr1 & 3) << 4) | (chr2 >> 4);
        enc3 = ((chr2 & 15) << 2) | (chr3 >> 6);
        enc4 = chr3 & 63;
        if (isNaN(chr2)) {
            enc3 = enc4 = 64
        } else if (isNaN(chr3)) {
            enc4 = 64
        }
        output = output + keyStr.charAt(enc1) + keyStr.charAt(enc2) + keyStr.charAt(enc3) + keyStr.charAt(enc4);
        chr1 = chr2 = chr3 = "";
        enc1 = enc2 = enc3 = enc4 = ""
    } while (i < input.length);
    return output
}
''')
    encode=jm.call('encodeInp',xh)+'%%%'+jm.call('encodeInp',mima)
    header={
   'Accept': 'text/html, application/xhtml+xml, application/xml; q=0.9, */*; q=0.8',
   'Accept-Encoding': 'gzip, deflate',
   'Accept-Language': 'zh-CN',
   'Connection': 'Keep-Alive',
   'Content-Type': 'application/x-www-form-urlencoded',
   'Cookie': co,
   'Host': 'inquiry.ecust.edu.cn',
   'Referer': 'http://inquiry.ecust.edu.cn/jsxsd/',
   'Upgrade-Insecure-Requests': '1',
   'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134'}
    data={
   'encoded': encode,
   'RANDOMCODE': yzm,
}
    url3='http://inquiry.ecust.edu.cn/jsxsd/xk/LoginToXk'
    d=s.post(url3,headers=header,data=data)
    url4='http://inquiry.ecust.edu.cn/jsxsd/kscj/cjcx_list'
    data={'kcmc':'','kcxz':'','kksj':'2017-2018-2','xsfs':'all'}
    e=s.post(url4,headers=header,data=data)
    ee=BeautifulSoup(e.text)
    str=''
    for z in ee.find_all('td'):
        str=str+z.get_text()+'\n'
    xunh=xunh+1
    if xunh>8:
        str='请重新尝试 检查密码是否错误'
    with open(sou+'.txt','w')as fss:
        fss.write(str)
    if str=='':
        jwcx(xh,mima,sou,xunh)

