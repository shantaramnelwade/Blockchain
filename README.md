# Blockchain
# Blockchain using current locations and timings.



import tkinter 
from tkinter.ttk import *
from tkinter import  *
import time as tm
import hashlib as hs
import folium
from folium import plugins
from folium.plugins import MeasureControl
from selenium import webdriver as wb
ass=wb.Chrome()
from selenium.webdriver.common import action_chains, keys
br=wb.Chrome()
wb.support.abstract_event_listener(br)
chrome_options = wb.ChromeOptions()
chrome_options.add_argument('--no-sandbox')
chrome = wb.Chrome('chromedriver', chrome_options=chrome_options)
#from selenium.webdriver.common.keys import Keys
#chrome.find_element_by_tag_name('body').send_keys(Keys.CONTROL + Keys.SHIFT + 'I')
chrome.get('file:///C:/Users/comp/Desktop/html%20to%20json/map.html')
chrome.get_log('browser')
action = action_chains.ActionChains(chrome)
action.send_keys(keys.Keys.F12)
action.release()


def newer():

    chrome_options = wb.ChromeOptions()
    chrome_options.add_argument('--no-sandbox')
    chrome = wb.Chrome('chromedriver', chrome_options=chrome_options)
    chrome.get('file:///C:/Users/comp/Desktop/html%20to%20json/map.html')
    chrome.get_log('browser')
    action = action_chains.ActionChains(chrome)
    action.send_keys(keys.Keys.F12)
    action.release()
    
import os
class blockchain(Tk):   

    def __init__(self):
        self.window=tkinter.Tk()
        self.window.geometry('500x400')
        self.window.title("BLOCKCHAIN TRANSACTION") 
        self.txt_id = Entry(width=10) 
        self.txt_id.grid(column=4, row=7)
        self.txt_name = Entry(width=10) 
        self.txt_name.grid(column=4, row=5)        
        self.id_lbl=Label(text="ENTER ID",font=("Arial Bold", 12))
        self.id_lbl.grid(column=4,row=6)               
        self.name_lbl=Label(text="ENTER NAME",font=("Arial Bold", 12))
        self.name_lbl.grid(column=4,row=4)
        self.pre_hash="0000" 
        #self.m = folium.Map(location=[18.5204,73.8567], tiles = 'OpenStreetMap',
           #                 zoom_start = 12, control_scale = True, prefer_canvas=True)
        #self.abc=self.m.add_child(folium.ClickForMarker())
        #self.ss=self.m.add_child(MeasureControl(self.abc.location))
        #self.naya ='mapp.html'
        #self.m.save(self.xy)         
        self.lis=[]
        self.button() 
        self.window.mainloop()
        
    def Data(self):
        self.tx_id=self.txt_id.get()# getting text id
        self.tx_name=self.txt_name.get()
        self.ct=tm.asctime()# getting current sysytem timing
        self.all=self.tx_id+self.tx_name+self.ct+self.pre_hash
        self.hashh = hs.md5()
        self.hashh.update(self.all.encode('utf-8'))
        self.h = hs.md5()
        self.h.update(self.pre_hash.encode('utf-8'))
        self.Pre_hash=self.h.hexdigest()
        print("PREVIOUS NAME: {}, NAME: {}, ID: {}, SYS CURRENT TIME: {}".format(self.pre_hash,self.tx_name,self.tx_id,self.ct))
        self.new_hash=self.hashh.hexdigest() 
        self.Key=self.Pre_hash+self.new_hash
        self.lis.append(self.Key)
        print(self.lis)
        self.pre_hash=self.new_hash     
    def Add_map(self):
        #print(self.lis) 
        self.chrome_options = wb.ChromeOptions()
        self.chrome_options.add_argument('--no-sandbox')
        self.chrome = wb.Chrome('chromedriver', chrome_options=self.chrome_options)
        self.aa=self.chrome.get('file:///C:/Users/NOOTBOOK/map.html')##copy the map URL i have provided and paste into that
    def Add_location(self):
        self.get_class_element=self.chrome.find_element_by_class_name('leaflet-popup-content')
        self.location= self.get_class_element.text
        print(self.location) 
        self.varr=self.location
        self.lis.append(self.location)
       # file:///C:/Users/NOOTBOOK/map.html
        self.chrome.close()     
    def button(self):        
        self.run=Button(command=self.Data,text="click")
        self.run.grid(column=4,row=8) 
        self.add_map=Button(command=self.Add_map,text='Add_map')
        self.add_map.grid(column=4,row=12)
        self.add_location=Button(command=self.Add_location,text="Add_location")
        self.add_location.grid(column=4,row=16)


a=blockchain()
