import requests
from bs4 import BeautifulSoup
import urllib3

FechaIni = '20190301'
FechaFin = '20190701'

Empresas = ['ALICORC1', 'BACKUSI1', 'BAP', 'BVN', 'CASAGRC1', 'CONCESI1', 'CONTINC1', 'CORAREI1', 'CPACASC1', 'CREDITC1', 'CVERDEC1']

urllib3.disable_warnings()

filename = "bvl_historico.csv"
# opening the file with w+ mode truncates the file
f = open(filename, "w+")
f.close()

cabecera = "Nemonico|Id|Fecha|Apertura|Cierre|Maxima|Minima|Promedio|CantidadNegociada|MontoNegociado|FechaAnterior|CierreAnterior"
fileA = open("bvl_historico.csv", "a+")
fileA.write(cabecera + "\n")
fileA.close()

for valores in Empresas:
  tabla = requests.get('https://www.bvl.com.pe/jsp/cotizacion.jsp?fec_inicio='+FechaIni+'&fec_fin='+FechaFin+'&nemonico='+valores,verify=False)
  soup = BeautifulSoup(tabla.text, 'html.parser')

  lista = []
  for index,i in enumerate(soup.find('table').findAll('tr')):
      file = open("bvl_historico.csv","a+")
      if index > 1:
          item = i.findAll('td')
          format =  "{0}|{1}|{2}|{3}|{4}|{5}|{6}|{7}|{8}|{9}|{10}|{11}".format(valores,index,item[0].text ,item[1].text , item[2].text, item[3].text, item[4].text, item[5].text, item[6].text, item[7].text, item[8].text, item[9].text)
          lista.append({
              'id': index,
              'name' : item[1].text
          })
          file.write(format + "\n")
          file.close()
          #print(format)
  #print(lista)
