# Vandalism:Web:250pts
Challenge instance ready at 95.216.233.106:24317.  
That admin panel was awfully bare. There must be some other page, but we've no idea where it is. Just to clarify, ractf{;)} is the greedy admins stealing all the flags, it's not the actual flag.  

# Solution
アクセスするとログインフォームが見える。  
Login  
[site1.png](../Entrypoint/site/site.png)  
`'`でエラーが出たので、SQLインジェクションを試みる。  
`' OR 't'='t`ではxxslayer420としてログインしてしまう。  
ではこれ以外のユーザーでのログインを試みる。  
ユーザー名がxxslayer420以外を指定する`' OR username!='xxslayer420`である。  
するとAdminでのログインが成功する。  
Welcome, jimmyTehAdmin  
[site2.png](../Admin_Attack/site/flag.png)  
adminのpanelを見つければいいようだ。  
X-OptionalHeaderにLocation: /__adminPortalが入っていた。  
通常は302でリダイレクトしてしまうがWelcome, jimmyTehAdminページからアクセスすると以下のページに飛ぶ。  
__adminPortal  
[site3.png](site/site3.png)  
ractf{;)}は違うらしい。  
ソースを見てみると以下のような不思議な文字が書き込まれている。  
__adminPortal(source)  
[site4.png](site/site4.png)  
よく見るとアルファベットが入っているようなので抜き出してみる。  
```bash
$ cat __adminPortal.html | tr -cd "abcdefghijklmnopqrstuvwxyz0123456789{}"
htmlheadmetanamecharsetvalueutf8linkhrefhttpsfontsgoogleapiscomcssfamilyanumothic400700displayswaprelstylesheetlinkrelstylesheethrefstaticfindexcsstitleogintitleheadbodydivclasscontainerprestylefontsize12pxfontfamilymonospacehisflaghasbeenvandalizednjoyreedyadminswantmoreflagsforthemselveshisisnttheflagtsjustmoreartpreh3styledisplaynoneoremipsumdolorsitametconsecteturadipiscingelituistinciduntuturnasedvehiculauncportaligulaegetleoposuerevelblanditanteiaculistiameteratnequeellentesquealiquetvelitmagnasitametconsecteturduifringillaidednonmassaauctorlaoreetmassaidplaceratsemroinneceliteurisusdignissimvestibulumeuaccumsannisiivamusvitaemaurisatmigravidaluctustiamimperdietliberoutnullavehiculaeleifendestibulumsitametipsumnisiamnecleolaciniafeugiatsemnecmolestiequamestibulumquamjustosuscipitsednisiinmolestiecondimentumestunccursussagittisnibhconvalliseuismodnisipulvinaratnconsequatnislidodioconsequatpretiumuisqueeteratinleoefficiturfaucibusellentesquevelgravidaenimsedpulvinartortorullammalesuadadignissimligulasitametdignissimtiamutexquamonecgravidarisusodioafringillaturpisportautedacrisusinloremtempussodalesuisaliquampellentesquemolestienhachabitasseplateadictumstuspendissenonrisusutloremullamcorpermalesuadaegetaliberoliquammassaloremhendreritinfeugiatsitametconsecteturquisnisiuissedligulalaoreetpretiumexutauctormassahasellusnonleoconsecteturlaciniavelitnonfermentumduiedaestsitameteroslobortisposuereegetsagittisliberohasellushendreritplaceratligulanonvenenatisraspulvinarleogravidaractf{h1dd3n1npl4n3s1ght}pharetrablandittiamluctusmieudolorvolutpatinterdumblanditarcumaximusrasvenenatissedligulaaeleifendestibulumanteipsumprimisinfaucibusorciluctusetultricesposuerecubiliauraeestibulumanteipsumprimisinfaucibusorciluctusetultricesposuerecubiliauraeestibulumidnislegetleoposueremalesuadaellentesquehabitantmorbitristiquesenectusetnetusetmalesuadafamesacturpisegestaseneansitametpretiumelitnmaximusscelerisqueodiosedelementumjustotemporeunultriceserosinlaciniaaliquamivamusmaximusfermentumenimsedconvallisedsuscipitligulasitametvelitfaucibusinterdumroinconguenullaornarepharetraconvallisnequeodiocursusdoloregetpretiumliberopurusveltortornnequearculuctusetjustosedauctorscelerisquenibhivamusacportafelisquistempormassauisquepretiumeuismodauguenonbibendumellentesqueeumetusidligulaultriciesegestasetinsapienuisquecondimentumduietpulvinarcongueuisaccumsaninterdummiquisluctusestibulumnonultricessemidsagittispurusonecconsequatestvitaetellusportanecornareauguefeugiatullah3divbodyhtml
$ cat __adminPortal.html | tr -cd "abcdefghijklmnopqrstuvwxyz0123456789{}" | grep -oP "ractf{.*?}"
ractf{h1dd3n1npl4n3s1ght}
```
flagが得られた。  

## ractf{h1dd3n1npl4n3s1ght}