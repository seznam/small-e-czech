# Small-E-Czech

Představujeme vám Small-E-Czech. A co to vlastně Small-E-Czech je? Jedná se o novou neuronovou síť natrénovanou v Seznamu. Ta je schopná řešit úlohy spjaté s porozuměním českému jazyku. Povedlo se nám díky ní zvýšit kvalitu výsledků vyhledávání nebo opravy překlepů. A teď ji máte od nás na Githubu k dispozici i vy.

## Jak se Small-E-Czech učí

Síť vychází z modelu [Electra](https://arxiv.org/abs/2003.10555) (varianta small) z roku 2020. Nejprve se předučí na velkém množství textu, čímž získá povědomí o fungování češtiny a významu slov, a následně se doučuje na konkrétní úlohu, která nás zajímá.


Vstupem do modelu je text rozdělený na tokeny algoritmem [Wordpiece](https://paperswithcode.com/method/wordpiece). Tokeny jsou celá slova (pokud se vyskytují často), nebo jen části slov až jednotlivé znaky, ze kterých se dají méně častá slova složit.


Předučení probíhá tak, že se neuronové síti ukazují věty, v nichž byly některé tokeny nahrazeny jinými. Síť má pak pro každý token rozhodnout, jestli je původní. Pokud se zmýlí, váhy spojení mezi neurony v síti (je jich zhruba 14 milionů) se mírně upraví tak, aby se příště spíš trefila, a pokračuje se další větou. Small-E-Czech se předučoval asi 20 dní za použití 250 GB textu na jedné grafické kartě.


Ve fázi doučení se nahradí koncová část sítě takovou, která má vhodný tvar pro danou úlohu (například vrací jen jedno číslo pro celý vstupní text, pokud chceme klasifikovat recenze na pozitivní a negativní) a následně se síť učí minimalizovat chyby na příslušných trénovacích datech (dvojicích tvořených vstupním textem a požadovanou odpovědí) podobně jako při předučení. Těchto trénovacích dat je obvykle relativně málo, protože správné odpovědi dodávají lidé. Doučení proto trvá kratší dobu (v našem případě jednotky až desítky hodin). Pro výslednou kvalitu je pak důležité, že síť nezačíná od nuly, ale nese si ve svých vahách znalost jazyka z fáze předučení.


Small-E-Czech je se svými 14 miliony vahami výrazně menší sítí než třeba původní anglický [BERT](https://arxiv.org/abs/1810.04805), který má vah 110 milionů. Větší sítě obvykle dosahují vyšší úspěšnosti, jejich nevýhodou je ovšem pomalejší učení i následné vyhodnocování.


## Začněte Small-E-Czech využívat i vy

V Seznamu jsme použili Small-E-Czech například jako vstup do modelu, který řadí výsledky vyhledávání. Podle našich měření víme, že jsme tak zvýšili kvalitu zobrazených výsledků v průměru o 4 %. Dodáváme pomocí něj také vektory pro dotazy a webové stránky do tzv. [vektorového hledání](https://blog.seznam.cz/2021/02/vyhledavani-pomoci-vyznamovych-vektoru/). Přispěl ke zlepšení oprav překlepů v dotazech, které jsou díky chytřejším návrhům průměrně o 30 % rychlejší a jednotky procent lepší (v pokrytí a přesnosti). Pro feed článků na homepage Seznamu s precision 99.5 % a recallem 85 %. Možnosti využití jsou zkrátka široké.


Abychom podpořili výzkum jazykových modelů pro češtinu a umožnili nasazení modelu Small-E-Czech i v oblastech, kterým se v Seznamu nevěnujeme, rozhodli jsme se jej zveřejnit – a to i pro komerční použití. Model snadno stáhnete z HuggingFace [repozitáře](https://huggingface.co/Seznam/small-e-czech), kde je i krátký návod, jak jej aplikovat na novou úlohu. Budeme rádi, když o nových aplikacích dáte vědět a třeba inspirujete další.
