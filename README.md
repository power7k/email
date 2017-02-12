# email

# -*- coding:utf-8 -*-

from email.header import Header
from email.mime.text import MIMEText
from email.utils import parseaddr, formataddr
import smtplib

def _format_addr(s): 
	name, addr=parseaddr(s)
	return formataddr((Header(name,'utf-8').encode(), addr.encode('utf-8') if isinstance(addr, unicode) else addr))

from_addr= '18356958782@163.com'
password='abcd1234'
to_addr='531196096@qq.com'
smtp_server='smtp.163.com'
stringtmp='English'
emailInfo = '测试一下中文和(%s)' % stringtmp
msg=MIMEText(emailInfo, 'plain', 'utf-8')
msg['From']=_format_addr(u'帅哥<%s>' % from_addr)
msg['To']=_format_addr(u'收件人<%s>' % to_addr)
msg['Subject']=Header(u'来自帅哥的邮件', 'utf-8').encode()
server=smtplib.SMTP(smtp_server,25)
server.set_debuglevel(1)
server.login(from_addr, password)
server.sendmail(from_addr, [to_addr], msg.as_string())
server.quit()
