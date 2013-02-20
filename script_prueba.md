script_dns
==========

Script para administrar DNS 

/usr/bin/python
import sys
import os
if sys.argv[1] == '-add':       #insertar registro
        tipo = sys.argv[2]
        if tipo == '-eq':  #quiere añadir una direccion de tipo A
                equipo = sys.argv[3] #nombre equipo
                ip = sys.argv[4]        #direccion ip
                insert =  equipo + '    A       ' + ip +'\n'    #resol directa
                f= open('/var/cache/bind/db.iestejero.com','a')
                f.write(insert)
                f.close
                ipin=ip.split('.') #separamos la ip por puntos
                ipfin=ipin[-1] #ultimos numeros de la ip
                inversa= ipfin + '      PTR     ' + equipo +'.iestejero.com' + '\n'
                f= open('/var/cache/bind/db.10.168.192') #fichero resol
                f.write(inversa)
                f.close
                os.system('/etc/init.d/bind9 restart')
        elif tipo == '-alias':          #insertar alias
                nombre = sys.argv[3]            #defino el nombre del alias
                host = sys.argv[4]              #defino el nombre del equipo
                insert = nombre + '     CNAME   ' + host + '\n'         #inserto linea
                f= open('/var/cache/bind/db.iestejero.com','a')         #abro fichero
                f.write(insert)                         #inserto lineas
                f.close                                 #cierro fichero
                os.system('/etc/init.d/bind9 restart')  #reinicio servicios

        else:
                print 'Algún parámetro no es correcto'
elif sys.argv[1] == '-del':
        if sys.argv[2] == '-direct': #si el segundo parametro es direct se buscara en el fichero de busqueda directa   
        delete == sys.argv[3]
                f = open('/var/cache/bind/db.iestejero.com','r') #abrimos el fichero
                lineas = f.readlines()
                for delete in lineas:
                        if delete.find
        elif sys.argv[2] == '-inver': #si el segundo parametro es inver se buscara en el fichero de busqueda inversa

        else:
                print 'A ocurrido un error al seleccionar el fichero donde buscar la palabra a eliminar'
else:
        print 'Algún parámetro no es correcto'

