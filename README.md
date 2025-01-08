#impordin teistest failist laused
from wordlist import sõnad
import random

#mehe kuju, vigade arv
mees = {0: ("",
            "",
            "",
            "",
            "",
            ""),
        1: ("",
            "",
            "",
            " o",
            ""
            ""),
        2: ("",
            "",
            "",
            " o",
            " |",
            ""),
        3: ("",
            "",
            "",
            " o",
            "/|",
            ""),
        4: ("",
            "",
            "",
            " o",
            "/|\\",
            ""),
        5: ("",
            "",
            "",
            " o",
            "/|\\",
            "/"),
        6: ("",
            "",
            "",
            " o",
            "/|\\",
            "/ \\"),
        7: ("",
            "",
            " |",
            " o",
            "/|\\",
            "/ \\"),
        8: ("",
            " |",
            " |",
            " o",
            "/|\\",
            "/ \\"),
        9: ("_",
            " |",
            " |",
            " o",
            "/|\\",
            "/ \\"),
        10: ("_ _",
            " |",
            " |",
            " o",
            "/|\\",
            "/ \\")}

#näitab meest vastavalt vigade arvule
def tore_mees(vale):
    print("       ")
    print("#######")
    for i in mees[vale]:
        print(i)
    print("#######")
    print("       ")
#näitab palju tähti lauses on   
def tore_vihje(vihje):
    print(" ".join(vihje))
#näitab vastust
def tore_vastus(vastus):
    print(" ".join(vastus))
#valib lause, loob selle järgi vihje, proovitud tähed jätab meelde
def main():
    vastus = random.choice(sõnad)
    vihje = ["_"] * len(vastus)
    vale = 0
    proovitud_tähed = set()
    is_running = True
    
#näitab lauses tühikuid
    for j in range(len(vastus)):
        if vastus[j] == " ":
            vihje[j] = " "

#näitab meest vigade arvu põhjal, näitab vihjet, küsib kasutajalt tähte            
    while is_running:
        tore_mees(vale)
        tore_vihje(vihje)
        proov = input("Sisesta täht: ").lower()
        
#kontrollib, et kasutaja sisestaks ainult ühe tähe ja et see oleks tähestikus
        if len(proov) != 1 or not proov.isalpha() :
            print("SELLINE VASTUS EI SOBI!")
            continue
#kontrollib, kas kasutaja on seda tähte juba proovinud        
        if proov in proovitud_tähed:
            print(f"{proov} <- SEDA TÄHTE OLED JUBA PROOVINUD!")
            continue
#lisab kasutaja poolt sisestatud tähe vihjesse        
        proovitud_tähed.add(proov)
#kui täht on õige, läheb see vihjes vastavasse kohta        
        if proov in vastus:
            for l in range(len(vastus)):
                if vastus[l] == proov:
                    vihje[l] = proov
#kui täht ei ole lauses, suureneb vigade arv                    
        else:
            vale += 1
#sõna on arvatud            
        if "_" not in vihje:
            tore_mees(vale)
            tore_vastus(vastus)
            print("TUBLI! ARVASID VANASÕNA ÄRA!")
            is_running = False
#sõna ei ole arvatud            
        elif vale >= len(mees) - 1:
            tore_mees(vale)
            tore_vastus(vastus)
            print("SA EI ARVANUD ÕIGET VANASÕNA ÄRA!")
            is_running = False
            
#käivitab           
if __name__ == "__main__":
    main()

