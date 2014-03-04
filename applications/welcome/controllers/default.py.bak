# -*- coding: utf-8 -*-
# this file is released under public domain and you can use without limitations

#########################################################################
## This is a sample controller
## - index is the default action of any application
## - user is required for authentication and authorization
## - download is for downloading files uploaded in the db (does streaming)
## - call exposes all registered services (none by default)
#########################################################################
response.title='WEP2PY HOŞGELDİNİZ'
import time
import random
def index():
    """
    example action using the internationalization operator T and flash
    rendered by views/default/index.html or views/generic.html

    if you need a simple wiki simply replace the two lines below with:
    return auth.wiki()
    """
    response.flash = T("Welcome to web2py!")
    return {'message':'Merhaba Dünya'}

def irfan():
    veri={}
    erisim=time.ctime()
    rast=random.random();
    veri['erisim']=erisim
    veri['rast']=rast
    veri['ad']='İrfan'

    """ Form Oluşturma işlemleri yapılıyor."""
##Ders: IS_LİST_OF Birden fazla requires yazmamızı sağlayan koddur. örnek: requires = IS_LIST_OF(IS_INT_IN_RANGE(0, 10))
    veri['form']=FORM('Adı:', INPUT(_name="adi",
                                    requires=IS_IN_SET(('ali','veli'),error_message='Bu isim listede yok')), # Bu alanda kullanılan 'IS_IN_SET' içindeki veriler girilirse veri girişi onaylanır. Girilmez ise hata mesajı alınır.

                     'Soyadı:', INPUT(_name='soyadi',
                                      requires=IS_NOT_EMPTY()), #Text girişi oluşturma
                      # IS_NOT_EMPTY() boş geçilemez anlamındadır.

                      SELECT('Artvin',
                             'Sinop',
                             'Samsun',
                             _name='il'), #Açılır list oluşturma
                      'YAŞ:', INPUT(_name='yas',
                                      requires=IS_INT_IN_RANGE()), # IS_INT_IN_RANGE(0,25)  bu aralıkta değer alır [0,24) ,IS_INT_IN_RANGE()
                      'Email:', INPUT(_name='email',
                                      requires=IS_EMAIL(error_message='Lütfen email adresinizi doğru bir şekilde yazınız')),
                      INPUT(_type='submit',
                           _value='Soruyu Gönder')
                      )

#####----Gelen veri dolumu boşmu kontrol etmek için amele işi ------###
        #    if request.vars:
        #       if request.vars.soyadi:
        #            response.flash = "Sen Bu İşi Biliyorsun"
        #        else:
        #            response.flash ="Etmaaaa Şans"

###--------------

### Form required kontrolu yapıldı form elemanlarına verilen 'requires=IS_NOT_EMPTY()' bu değer ve aşağıdaki kodlar sayesinde###

    if veri['form'].process().accepted:
        #response.flash='sen bu işi biliyorsun kardeşim.' #flash messaj oluştur.
        #redirect(URL('/tamam')) #Yönlendirme yapılır. bu alandaki 'tamam' bir işlevin karşılığıdır.
        if int(request.vars.yas)<=18:
            response.flash='Adam ol gel!!!'
        else:
            response.flash='Adamsın!!!'
    else:
        response.flash='Bir yanlışlık var herhalde!!!'

###-----------------

    return veri

def tamam():
    
    return "<h1>KAYIT BAŞARILI</h1>"

def user():
    """
    exposes:
    http://..../[app]/default/user/login
    http://..../[app]/default/user/logout
    http://..../[app]/default/user/register
    http://..../[app]/default/user/profile
    http://..../[app]/default/user/retrieve_password
    http://..../[app]/default/user/change_password
    http://..../[app]/default/user/manage_users (requires membership in
    use @auth.requires_login()
        @auth.requires_membership('group name')
        @auth.requires_permission('read','table name',record_id)
    to decorate functions that need access control
    """
    return dict(form=auth())

@cache.action()
def download():
    """
    allows downloading of uploaded files
    http://..../[app]/default/download/[filename]
    """
    return response.download(request, db)


def call():
    """
    exposes services. for example:
    http://..../[app]/default/call/jsonrpc
    decorate with @services.jsonrpc the functions to expose
    supports xml, json, xmlrpc, jsonrpc, amfrpc, rss, csv
    """
    return service()


@auth.requires_signature()
def data():
    """
    http://..../[app]/default/data/tables
    http://..../[app]/default/data/create/[table]
    http://..../[app]/default/data/read/[table]/[id]
    http://..../[app]/default/data/update/[table]/[id]
    http://..../[app]/default/data/delete/[table]/[id]
    http://..../[app]/default/data/select/[table]
    http://..../[app]/default/data/search/[table]
    but URLs must be signed, i.e. linked with
      A('table',_href=URL('data/tables',user_signature=True))
    or with the signed load operator
      LOAD('default','data.load',args='tables',ajax=True,user_signature=True)
    """
    return dict(form=crud())
