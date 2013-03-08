from django.template.loader import get_template
from django.template import Context
from django.http import HttpResponse
#from paint1.models import Image

def mainPage(request):
    if request.method=='GET':
        h = get_template('paint.html')
        html = h.render(Context({}))
        return HttpResponse(html)

def loadPage(request,filename):
    if request.method=='GET':
        data=Image.objects.filter(name=filename)
        h = get_template('paint.html',lis=filename,imagedata=wholedata)
        html = h.render(Context({}))
        if data:
            html="""<script>var data=JSON.parse(' """+data[0].data+""" ');</script>"""+html
        else:
            html="""<script>alert("Image not found")</script>"""+html
        return HttpResponse(html)
    else:
        imgname=request.POST.get('filename')
        imgdata=request.POST.get('wholedata')
        try:
            f = Image.objects.get(name=imgname)
        except Image.DoesNotExist:
            f=Image(name=imgname,data=imgdata)
            f.save()
        else:
            f.data=imgdata
            f.save()
