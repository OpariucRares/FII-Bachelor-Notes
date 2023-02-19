----
## Care sunt ideile principale ale acestui model?
 - 1992 bazele; 2000 - apare RBAC-ul consolidat
 - **Ideea**: nu acorzi drepturile pe subiect/grupe de subiecte, ci pe rolul pe care il poate juca un subiect in sistem
 - roluri stabile, grupurile se pot modifica frecvent
## Care sunt componentele?
 - componente statice: useri, roluri, permisiuni si relatia dintre ei (se modifica rar)
 - componente dinamice: subiecte, autorizare de rol si autorizare acces pe obiect
## Care sunt elementele
 - User: persoana care deschide un dispozitiv de calcul
 - Rol: actiuni ce trebuie intreprinse in cadrul sistemului de unul sau mai multi utilizatori
 - Permisiuni: descrieri ale actiunilor care pot fi executate in cadrul unui rol (r, w, x, etc)
	 - sunt considerate pozitive si nu negatie (de exempli nu ai voie sa faci asta)
 - Aspectul negativ e surprins de restrictii de autorizare pe rol
 - Un utilizator poate juca mai multe roluri, un rol poate fi jucat de mai multi utilizatori
## Cum este reprezentat matematic acest model?
 - $UR(u) = {r \in R \space | \space (u, r) \in UR}$
 - $UR(r)^{-1} = {u \in U \space |\space (u, r) \in UR}$ 
 - $RP \subseteq R \times P$
 - RP(r) -> permisiuni asociate unui rol
 - $RP(r)^{-1}$-> rolurile asociate pentru o permisiune
## Ce reprezinta un subiect?
 - Subiect = proces/program care actioneaza pentru un utilizator
## Cum este reprezentat matematic un subiect?
 - sub=sesiune in care user-ul vb cu sistemul
 - su: S -> U
 - su(s)=u: subiectul s lucreaza in locul utilizatorlui u
 - subiectul mosteneste din rolurile utilizatorului in locul caruia joaca (proprietatea de autorizare pe rol)
## Cum se realizeaza autorizarea pentru accesarea unui obiect?
 - access(s, op, o) => $\exists$ un rol r $\in$ R, $\exists$ o permisiune p $\in$ P: r $\in$ SR(s), p $\in$ RP(r), p -> (op, o)
 - accesul se face daca exista un rol r si permisiunea p, iar r apartine sesiunii si are permisiune utilizatorul, atunci se face operatia					

## Ce tipuri de RBAC exista?
 - Ierarhii pe roluri
 - RBAC cu constrangeri

## Ce este RBAC cu ierarhii pe roluri?
 - pot restrictiona fluxul de informatii si este mai usoara implementarea, deoarece
se pot mosteni proprietatile
 - r1$\geq$r2 -> r1 mosteneste permisiunile din r2

## Cum se realizeaza autorizarea pentru acest model?
 - Autorizare user-ul u pt rolul r: {u $\in$ U | $\exists$ r': (u, r') $\in$ UR $\cap$ r'$\geq$r}
	- un user este autorizat pentru un rol r daca userul are un rol r' ce il mosteneste pe r
	- user cu roluri puternice -> nu joaca un rol slab
## Cum se realizeaza permisiunea p pentru rolul r?
 - Permisiunea p pentru rolul r: $\exists$ r' $\in$ R a.i. p $\in$ RP(r') si r' $\leq$ r
 - daca permisiunea p este asignat unui rol r' care este mostenit de r
	
## Ce este RBAC cu constrangeri?
 - simplifica designul, un mai bun view asupra sistemului, aduce mai multa putere
 - permite creare de roluri si permisiuni cu excludere mutuala
 - controleaza oferirea de roluri per user sau permisiuni per role

## Cum se aplica Separation of Duty?
 - static - pune constrangeri pe roluri pe care user-ul este autorizat pe roluri (SSD)
	- profesor Bob nu poate fi la examinare sau supraveghere contestatii 
- dinamic - invocate cand userul foloseste activ sistemul (DSD)
	- profesor Bob poate fi la examinare sau supraveghere contestatii, dar nu in aceeasi sesiune
- operational SoD (OSD) - niciun user nu poate toate actiunile critice intr-o functie

## Cum se creeaza un RBAC consolidat?
 - Ierarhie pe roluri + Restrictii = RBAC consolidat

## Implementari
- Windows si UNIX OS

## Concluzie RBAC
- DAC si MAC nu sunt flexibile
- RBAC poate fi combinar cu DAC si MAC, dar in practica nu vrem sa le eliminam


