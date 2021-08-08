import webbrowser
import time
import math
# importing webdriver from selenium 
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import NoSuchElementException
from selenium.common.exceptions import StaleElementReferenceException

from pygame._sdl2 import get_num_audio_devices, get_audio_device_name #Get playback device names
from pygame import mixer #Playing sound


url = 'https://accounts.google.com/signin/v2/identifier?ltmpl=meet&continue=https%3A%2F%2Fmeet.google.com%3Fhs%3D193&&flowName=GlifWebSignIn&flowEntry=ServiceLogin'




# Here Chrome will be used 
#driver = webdriver.Chrome("D://openlink_meet/chromedriver.exe")
chrome_options = Options()
#chrome_options.add_argument('use-fake-device-for-media-stream')
chrome_options.add_argument('use-fake-ui-for-media-stream')
chrome_options.add_argument('--disable-notifications')
driver = webdriver.Chrome("Enter your path to chrome driver",chrome_options=chrome_options)



# Opening the website 
driver.get(url) 

# geeting the button by class name 
SignIn = driver.find_element_by_id("identifierId") 

# clicking on the button 
SignIn.send_keys("your email here")
SignIn.send_keys(Keys.ENTER)

driver.implicitly_wait(10)

EnterPass =driver.find_element_by_xpath("//*[@id='password']/div[1]/div/div[1]/input")
EnterPass.send_keys("your password here")
EnterPass.send_keys(Keys.ENTER)
EnterCode =driver.find_element_by_xpath("//*[@id='i3']")
EnterCode.send_keys("Enter the meet code here")
JoinLink =driver.find_element_by_xpath("/html/body/c-wiz/div/div[2]/div/div[1]/div[3]/div/div[2]/div[2]/button/span") 
JoinLink.click()



#Dismiss =driver.find_element_by_xpath("//*[@id='yDmH0d']/div[3]/div/div[2]/div[3]/div")
#Dismiss.click()
ignored_exceptions=(NoSuchElementException,StaleElementReferenceException)
#driver.implicitly_wait(10)
Mute = driver.find_element_by_xpath("//*[@id='yDmH0d']/c-wiz/div/div/div[9]/div[3]/div/div/div[4]/div/div/div[1]/div[1]/div/div[4]/div[1]/div/div/div")
Mute.click()

CamOff = driver.find_element_by_xpath("/html/body/div/c-wiz/div/div/div[9]/div[3]/div/div/div[4]/div/div/div[1]/div[1]/div/div[4]/div[2]/div/div")
CamOff.click()

#driver.implicitly_wait(10)



JoinNow =WebDriverWait(driver,10,ignored_exceptions=ignored_exceptions).until(EC.element_to_be_clickable((By.XPATH, "/html/body/div[1]/c-wiz/div/div/div[9]/div[3]/div/div/div[4]/div/div/div[2]/div/div[2]/div/div[1]/div[1]/span/span")))
JoinNow.click()

TurnOnCaptions = driver.find_element_by_xpath("/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[10]/div[2]/div/div[3]/div/span/button/span[2]")
TurnOnCaptions.click()
#ShowEveryone = driver.find_element_by_xpath("//*[@id='ow3']/div[1]/div/div[5]/div[3]/div[6]/div[3]/div/div[2]/div[1]/span")
#ShowEveryone.click()

students=WebDriverWait(driver,20,ignored_exceptions=ignored_exceptions).until(EC.element_to_be_clickable((By.XPATH, "/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[10]/div[3]/div[2]/div/div/div[2]/div/div")))
text = students.text
Total_numStudents = int(text)
print(Total_numStudents)

Caption_tray = WebDriverWait(driver,100,ignored_exceptions=ignored_exceptions).until(EC.presence_of_element_located((By.XPATH, "/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[7]/div")))
Captions = WebDriverWait(driver,100,ignored_exceptions=ignored_exceptions).until(EC.presence_of_element_located((By.XPATH, "/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[7]/div/div[2]/div/span/span")))
count = 0

staleElement = True
while staleElement :

        try :

            Caption_tray = driver.find_element_by_xpath("/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[7]/div")
            Captions = driver.find_element_by_xpath("/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[7]/div/div[2]/div")
            if Captions.is_displayed() :
                    Caption_text= Captions.text
                    Caption_text = Caption_text.lower()
                    print(Caption_text)
                    
                    
        except(StaleElementReferenceException):

            staleElement = True

        except(NoSuchElementException) :
                staleElement = True

        changed_numstudents = int(students.text)
        print(changed_numstudents)
        if changed_numstudents > Total_numStudents :
                Total_numStudents = changed_numstudents
        elif changed_numstudents < Total_numStudents :
        
                if changed_numstudents <= math.floor(0.2*Total_numStudents):  
                                EndCall=driver.find_element_by_xpath("/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[10]/div[2]/div/div[7]/span/button/i")
                                EndCall.click()
                        
                


        if count ==0 :

                 words = ("roll number 22", "Jondoe" , "Johndoe" , "Jon Doe" ,"June Doe" , "Jon" )
                 if any(name in Caption_text for name in words): 

                        UnMute = driver.find_element_by_xpath("/html/body/div[1]/c-wiz/div[1]/div/div[9]/div[3]/div[10]/div[2]/div/div[1]/div/div/span/button/div[2]")
                        UnMute.click()
                        mixer.init(devicename='CABLE Input (VB-Audio Virtual Cable)')
                        mixer.music.load("Enter path of your voice recording here")
                        mixer.music.play()
                        time.sleep(4)
                        mixer.music.stop()
                        UnMute.click()
                        count+=1
