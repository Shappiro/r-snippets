library(XML)
library(ldplyr)
library(RCurl)

urlStazioni<-'http://dati.meteotrentino.it/service.asmx/listaStazioni'
stazioni<-RCurl::getURLContent(urlStazioni)
stazioni<-xmlToDataFrame(stazioni)
# rimuovo le stazioni dismesse
stazioni<-stazioni[stazioni$fine!='',]
stazioniAttive<-as.character(stazioni$codice)

for(stazione in stazioniAttive[186]) {
	url<-paste0('http://dati.meteotrentino.it/service.asmx/ultimiDatiStazione?codice=',stazione)
	datastaz<-RCurl::getURLContent(url)
	datastaz<-ldply(
			xmlToList(datastaz),
			function(x) { data.frame(x) }
		)
	print(url)
}