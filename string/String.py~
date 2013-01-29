import webapp2
import random
import cgi

from google.appengine.api import users
from google.appengine.ext import db
c=0
class Data(db.Model):
	string1=db.StringProperty(multiline=True)
	countalpha = db.StringProperty()
	countdigit = db.StringProperty()
class MainPage(webapp2.RequestHandler):
	def get(self):
		self.response.out.write("""
          	<html>
            	<body bgcolor="orange">
		<br/><br/><br/><br/><br/><br/><br/><br/>
		<center>
		<font color="green">Enter and input the string</font>
		<table>
		<tr>
              	<form >
                <div><textarea name="string1" rows="3" cols="100"></textarea></div>
                <div><input type="submit" value="Input" style="background-color:orange"></div>
		<br/></br></br>
              	</form>
		</tr>
		<font color="green">Enter the string and get the count</font>
		<tr>
		<form >
                <div><textarea name="getcount" rows="3" cols="100"></textarea></div>
                <div><input type="submit" value="Get" style="background-color:orange"></div>
              	</form>
		</tr>
		</table></center>""")
		string1=self.request.get('string1')
		getcount=self.request.get('getcount')
		l = len(string1)
		counta=0
		countd=0
		for i in string1:		
			if i.isalpha():
				counta +=1 
			if i.isdigit():
				countd +=1
		countalpha = str(counta)
		countdigit = str(countd)
		if string1 != "":
			obj=Data(db.Key.from_path('Table',string1))
			obj.string1=string1
			obj.countalpha=countalpha
			obj.countdigit=countdigit
			getdata=db.GqlQuery("SELECT * FROM Data WHERE ANCESTOR IS :a",a=db.Key.from_path('Table',string1))
			cnt =0
			for i in getdata:
				cnt=cnt+1
			if cnt==0:
				obj.put()
			getdata1=db.GqlQuery("SELECT * FROM Data WHERE ANCESTOR IS :a",a=db.Key.from_path('Table',string1))
			
			for i in getdata1:
				self.response.out.write("""<br><br><br>""")
				self.response.out.write("""<center><br><font color="white">STRING: </font>""")
				self.response.out.write("<font size='5px' color='green'>"+i.string1+"</font>")
				self.response.out.write("""<br><font color="white">ALPHA COUNT: </font>""")
				self.response.out.write("<font size='5px' color='green'>"+i.countalpha+"</font>")
				self.response.out.write("""<br><font color="white">DIGIT COUNT: </font>""")
				self.response.out.write("<font size='5px' color='green'>"+i.countdigit+"</font>")
				self.response.out.write("</center>")
		
		fetch=Data.all()
		for i in fetch:
			if getcount == i.string1:
				self.response.out.write("""<br><br><br>""")
				self.response.out.write("<center>")
				self.response.out.write("""<br><font color="white" >STRING: </font>""")
				self.response.out.write("<font size='5px' color='red'>"+i.string1+"</font>")
				self.response.out.write("""<br><font color="white">ALPHA COUNT: </font>""")
				self.response.out.write("<font size='5px' color='red'>"+i.countalpha+"</font>")
				self.response.out.write("""<br><font color="white">DIGIT COUNT: </font>""")
				self.response.out.write("<font size='5px' color='red'>"+i.countdigit+"</font>")
				self.response.out.write("""<br></center>""")
		self.response.out.write("""</body></html>""")
	
app=webapp2.WSGIApplication([('/.*',MainPage)],debug=True)	
