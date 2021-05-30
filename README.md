# automate-gmail
# automated emailing 
import smtplib
import pyttsx3 as os
import speech_recognition as sr
import winsound

r = sr.Recognizer()
with sr.Microphone() as source2:
counter = os.init()
counter.setProperty('rate',145)
counter.say("hello i am pretty and i have been designed to make sending emails pretty simple for you")
counter.say("please say the email username to whoome you want to send the email after the beep")
counter.runAndWait()
counter.stop()
winsound.Beep(2500, 1000)
r.adjust_for_ambient_noise(source2, duration=1)
audio1 = r.listen(source2)
id = r.recognize_google(audio1)
print(id)

counter.say("please describe the subject of the email after the beep")
counter.runAndWait()
counter.stop()
winsound.Beep(2500, 1000)
r.adjust_for_ambient_noise(source2, duration=1)
audio2 = r.listen(source2)
sub = r.recognize_google(audio2)

counter.say("please speak the body of the email after the beep")
counter.runAndWait()
counter.stop()
winsound.Beep(2500, 1000)
r.adjust_for_ambient_noise(source2, duration=1)
audio3 = r.listen(source2)
text = r.recognize_google(audio3)

a = '@gmail.com'
b = id+a
x = b.replace(' ', '')
print(x)

y = sub.upper()

z = text
print(b)

gmail_user = 'user email'
gmail_password = 'user password'

sent_from = gmail_user
to = [x]
subject = y
body = z

email_text = """\
From: %s
To: %s
Subject: %s

%s
""" % (sent_from, ", ".join(to), subject, body)
try:
    server = smtplib.SMTP_SSL('smtp.gmail.com', 465)
    server.ehlo()
    server.login(gmail_user, gmail_password)
    server.sendmail(sent_from, to, email_text)
    server.close()

    counter.say("email sent")
    counter.runAndWait()
    counter.stop()
except:
    counter.say("Something went wrong")
    counter.runAndWait()
    counter.stop()
