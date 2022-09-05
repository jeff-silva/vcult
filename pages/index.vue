<template>
  <div>
    <div class="d-flex">
      <div class="flex-grow-1">
        <l-map v-bind="mapBind" style="width:100%; height:100vh;">
          <l-tile-layer url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"></l-tile-layer>
          <template v-for="(p, i) in places">
            <l-marker :key="i" :lat-lng="p.coords"></l-marker>
          </template>
        </l-map>
      </div>

      <div class="scroll-bottom" style="min-width:400px; max-width:400px; height:100vh; overflow:auto;">
        <template v-for="(p, i) in placesWithEvents">
          <div :key="i" class="pa-2 pb-0 font-weight-bold text-uppercase">{{ p.name }}</div>

          <template v-for="(e, ii) in p.events">
            <div :key="`${ii}-${i}`" class="pa-2">
              <div>{{ e.datetime }}</div>
              <div v-if="e.fullDay">24Hrs</div>
              <div>{{ e.name }}</div>
              <div v-if="e.place.name && e.place.name!=p.name" class="text--secondary" style="font-size:70%;">{{ e.place.name }}</div>
            </div>
          </template>
        </template>

        <div class="pa-3">{{ events.length }} eventos</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mapBind: {
        zoom: 15,
        center: [-19.912998, -43.940933],
      },
      places: [
        this.placeDefault({coords: [-19.9168340, -43.933900], id: "praca-estacao", name: "Praça da estação"}),
        this.placeDefault({coords: [-19.9168340, -43.933900], id: "palco-estacao", name: "Palco da Estação"}),
        this.placeDefault({coords: [-19.915440, -43.9360780], id: "palco-guaicurus", name: "Palco Guaicurus"}),
        this.placeDefault({coords: [-19.919453, -43.9337030], id: "arcos-viaduto", name: "Arcos do Viaduto"}),
        this.placeDefault({coords: [-19.919798, -43.9342730], id: "palco-arcos", name: "Palco Arcos"}),
        this.placeDefault({coords: [-19.919453, -43.9337030], id: "arcos-djs", name: "Arcos DJs"}),
        this.placeDefault({coords: [-19.919747, -43.9342040], id: "espaco-viralata", name: "Espaço Vira-lata"}),
        this.placeDefault({coords: [-19.919453, -43.9337030], id: "arcos-literatura", name: "Arcos da Literatura"}),
        this.placeDefault({coords: [-19.919677, -43.9342350], id: "palco-viaduto", name: "Palco Viaduto (Embaixo do viaduto)"}),
        this.placeDefault({coords: [-19.926497, -43.9333320], id: "parque-municipal-palco-gramado", name: "Parque Municipal (Palco Gramado)"}),
        this.placeDefault({coords: [-19.923948, -43.9349770], id: "parque-municipal-palco-parque", name: "Parque Municipal (Palco Parque)"}),
        this.placeDefault({coords: [-19.924390, -43.9351750], id: "parque-municipal-circuito-parque", name: "Parque Municipal (Circuito Parque)"}),
        this.placeDefault({coords: [-19.922463, -43.9342940], id: "parque-municipal-cine-parque", name: "Cine Parque (GRAMADO DO LAGO DOS BARCOS À REMO)"}),
        this.placeDefault({coords: [-19.918010, -43.9347250], id: "avenida-andradas-367", name: "AVENIDA DOS ANDRADAS, 367"}),
        this.placeDefault({coords: [-19.916612, -43.9347870], id: "praca-rui-barbosa", name: "PRAÇA RUI BARBOSA"}),
        this.placeDefault({coords: [-19.920942, -43.9364940], id: "rua-tamoios-lateral-parque", name: "RUA DOS TAMOIOS, LATERAL DO PARQUE MUNICIPAL"}),
        this.placeDefault({coords: [-19.918764, -43.9342460], id: "rua-aarao-reis", name: "RUA AARÃO REIS"}),
        this.placeDefault({coords: [-19.919244, -43.9383880], id: "escada-cine-theatro", name: "Escada Cine Theatro (Praça Sete, em frente ao Cine Theatro Brasil Vallourec)"}),
        this.placeDefault({coords: [-19.918566, -43.9355450], id: "espaco-forro", name: "Espaço Forró (RUA DA BAHIA COM RUA DOS TUPINAMBÁS)"}),
      ],
      events: [
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"praca-estacao"}, fullDay: true, name: "CURA - INSTALAÇÃO “ENTIDADES DE JAIDER ESBELL"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"praca-estacao"}, fullDay: true, name: "FUTEBOL DE SABÃO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"praca-estacao"}, fullDay: true, name: "ANTÔNIA MUNIZ - EXPOSIÇÃO \"FISSURADA\" - PRONTUÁRIO POÉTICO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"praca-estacao"}, fullDay: false, name: "VJS 1MPAR, HOMEM GAIOLA, BAH E PEDREIRO - LIVE MAPPING"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"praca-estacao"}, fullDay: false, name: "BH FIXED - 2o ALLEYCAT: OCUPA BH SOBRE DUAS RODAS"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"praca-estacao"}, fullDay: false, name: "PRAIA DA ESTAÇÃO"}),
        this.eventDefault({date_start: "2022-09-04 09:30:00", date_final: false, place: {id:"praca-estacao"}, fullDay: false, name: "TOTÓ HUMANO - ROBERT CECÍLIO"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"praca-estacao"}, fullDay: false, name: "ESCOLA BIKE ANJO - ENSINANDO A PEDALAR"}),
        this.eventDefault({date_start: "2022-09-04 11:50:00", date_final: false, place: {id:"praca-estacao"}, fullDay: false, name: "CIA. TODA DESEO - CAMPEONATO INTERDRAG DE GAYMADA"}),

        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "ORQUESTA ATÍPICA DE LHAMAS"}),
        this.eventDefault({date_start: "2022-09-03 20:30:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "CLARA X SOFIA - “NADA DISSO É PRA VOCÊ”"}),
        this.eventDefault({date_start: "2022-09-03 21:50:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "LAMPARINA"}),
        this.eventDefault({date_start: "2022-09-03 23:00:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "FESTA ELEGANZA NA VIRADA CULTURAL"}),
        this.eventDefault({date_start: "2022-09-04 01:30:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "FESTA MASTERPLANO - SHOWCASE"}),
        this.eventDefault({date_start: "2022-09-04 06:50:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "FESTA @BSURDA"}),
        this.eventDefault({date_start: "2022-09-04 14:30:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "FESTA TRANSA! “CAROLINA É UMA MENINA BEM DIFÍCIL DE ESQUECER”"}),
        this.eventDefault({date_start: "2022-09-04 19:00:00", date_final: false, place: {id:"palco-estacao"}, fullDay: false, name: "RENEGADO CONVIDA SANDRA DE SÁ"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "KAINNÁ TAWÁ - “POR TRÁS DAS PALAVRAS”"}),
        this.eventDefault({date_start: "2022-09-03 20:30:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "ELISA DE SENA (Festival Azeda)"}),
        this.eventDefault({date_start: "2022-09-03 21:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "PAJÉ E A NAVE (Festival Azeda)"}),
        this.eventDefault({date_start: "2022-09-03 23:00:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "BRANDU (Festival Azeda)"}),
        this.eventDefault({date_start: "2022-09-04 00:15:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "BRONKA (Festival Azeda)"}),
        this.eventDefault({date_start: "2022-09-04 02:15:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "LAURA SETTE (Festival Azeda)"}),
        this.eventDefault({date_start: "2022-09-04 03:30:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "X SEM PEITA (Festival Azeda)"}),
        this.eventDefault({date_start: "2022-09-04 04:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "MUVUKA (Festival Azeda)"}),
        this.eventDefault({date_start: "2022-09-04 06:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "MC RENATINHA SISTEMA 5S - “O FUNK É A COLA DA CIDADE PARTIDA”"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "BREEZY ON - NUMBER ONE"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "MALACA - PREFÁCIO"}),
        this.eventDefault({date_start: "2022-09-04 09:55:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "ABERTURA INDÍGENA (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 10:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "LUA ZANELLA (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 11:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "FLÁVIA ELLEN (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 12:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "MAÍRA BALDAIA (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 13:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "AMORINA CONVIDA MANGAIA (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 14:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "DEH MUSS (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 15:45:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "MAC JULIA (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 16:55:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "BIA NOGUEIRA (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 17:55:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "DORALYCE - SHOW DÁDIVA (Festival Sonora)"}),
        this.eventDefault({date_start: "2022-09-04 19:25:00", date_final: false, place: {id:"palco-guaicurus"}, fullDay: false, name: "PAIGE"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: true, name: "EXPOSIÇÃO DE CARROS ANTIGOS"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: true, name: "VERSO ESTÚDIO CRIATIVO - IMAGINÁRIOS URBANOS"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: true, name: "ENTREMEIO ESTÚDIO CRIATIVO - ESPAGUETE CRIATIVO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: true, name: "JULIANISMO - INSTALAÇÃO CORPO HISTÓRIA"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: true, name: "LIVELYYY - ALIANÇA FRANCESA"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: true, name: "EXPOSIÇÃO BH É QUEM? - FESTIVAL FORA DA CENA"}),
        this.eventDefault({date_start: "2022-09-03 20:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "ISABELA SOLO - NA VIRADA É MAIS GOSTOSO"}),
        this.eventDefault({date_start: "2022-09-03 20:30:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "GRUPO IDENTIDADE - FORMAÇÃO BLACK BLOC"}),
        this.eventDefault({date_start: "2022-09-03 23:10:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "ANDRÉ CALTON - A BOLHA"}),
        this.eventDefault({date_start: "2022-09-04 00:30:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "NAYARA CAMARGOS - QUANDO DESPERTO"}),
        this.eventDefault({date_start: "2022-09-04 01:45:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "GALLA ONFIRE - “ZONA AUTÔNOMA”"}),
        this.eventDefault({date_start: "2022-09-04 06:15:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "KAMALAKSI RUPINI - DANÇA CLÁSSICA INDIANA"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "II MUNDIALITO DE ROLIMÃ"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "LIBRÁRIO NA RUA - OFICINA DE LIBRAS"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "MOSTRAS:\nPIOLHO NABABO - RESIDÊNCIA TROCA-TROCA\nARTE TRAÇOS\nPÓ DE NUVEM BAZAR ITINERANTE\nOLHARES\nECONOMIA SOLIDÁRIA"}),
        this.eventDefault({date_start: "2022-09-04 16:30:00", date_final: false, place: {id:"arcos-viaduto"}, fullDay: false, name: "ANDRÉ CALTON - A BOLHA"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "BRUNO CUPERTINO - OBRAS PRIMAS - O SAMBA DE PAULINHO DA VIOLA"}),
        this.eventDefault({date_start: "2022-09-03 21:30:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "COLETIVO DOCILARÉ"}),
        this.eventDefault({date_start: "2022-09-03 23:45:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "SAMBA DA MEIA NOITE APRESENTA: SAMBA DE CABOCLO"}),
        this.eventDefault({date_start: "2022-09-04 07:45:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "FORRÓ CABRA CEGA"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "ORQUESTRA BIOS - CORPO DE BOMBEIROS MILITAR DE MINAS GERAIS"}),
        this.eventDefault({date_start: "2022-09-04 11:30:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "JULIANA ARAÚJO"}),
        this.eventDefault({date_start: "2022-09-04 14:00:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "GRUPO AXTRAL"}),
        this.eventDefault({date_start: "2022-09-04 15:30:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "IMANE RANE - “TEM QUE TER GANA”"}),
        this.eventDefault({date_start: "2022-09-04 16:50:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "RUADOIS"}),
        this.eventDefault({date_start: "2022-09-04 17:50:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "MONSTRA - FESTIVAL DE DANÇA DE SALÃO CONTEMPORÂNEA - CIA. DOIS RUMOS E DJ FIDELIS - “BAILE CONTEMPORÂNEO”"}),
        this.eventDefault({date_start: "2022-09-04 19:50:00", date_final: false, place: {id:"palco-arcos"}, fullDay: false, name: "BANDA UNIÓN LATINA - “JUNTOS A BAILAR!”"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"arcos-djs"}, fullDay: false, name: "DJ DIPOLAIR - ALIANÇA FRANCESA"}),
        this.eventDefault({date_start: "2022-09-03 20:30:00", date_final: false, place: {id:"arcos-djs"}, fullDay: false, name: "BAILE ROOM - BAILE DA VIRADA"}),
        this.eventDefault({date_start: "2022-09-04 00:30:00", date_final: false, place: {id:"arcos-djs"}, fullDay: false, name: "DJ AKILA"}),
        this.eventDefault({date_start: "2022-09-04 04:30:00", date_final: false, place: {id:"arcos-djs"}, fullDay: false, name: "BRUNO DUB DJ"}),
        this.eventDefault({date_start: "2022-09-04 08:30:00", date_final: false, place: {id:"arcos-djs"}, fullDay: false, name: "PALOMITA DJ"}),
        this.eventDefault({date_start: "2022-09-04 12:30:00", date_final: false, place: {id:"arcos-djs"}, fullDay: false, name: "RUA DO BASS"}),
        this.eventDefault({date_start: "2022-09-04 16:30:00", date_final: false, place: {id:"arcos-djs"}, fullDay: false, name: "ALTA FIDELIDADE - 100% VINIL"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: true, name: "THE PET LADY BH"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: true, name: "CÃOVIVER E LAR DE LUÍSA - GALERIA DE ADOÇÃO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: true, name: "TERRAL E JARDIM PARA TODOS - VÍDEOS COM DICAS DE PLANTIO E MANEJO DE CACTOS E SUCULENTAS"}),
        this.eventDefault({date_start: "2022-09-04 07:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "VARAL/MURAL DE ADOÇÃO DE PETS"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "ESPAÇO SPECIAL DOG • PETISCOS PET"}),
        this.eventDefault({date_start: "2022-09-04 08:30:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "VETERINÁRIA UNIBH • DICAS PARA TUTORES E SEUS PETS"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "CÃO DE RODINHAS BH • ENCONTRO DE PETS MAIS QUE ESPECIAIS"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "BATE-PAPO SOBRE PROTEÇÃO E ADOÇÃO • CÃOVIVER E LAR DE LUÍSA"}),
        this.eventDefault({date_start: "2022-09-04 11:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "REDE LIXO ZERO SANTA TEREZA • COMPOSTAGEM: COMO FAZER NA SUA CASA"}),
        this.eventDefault({date_start: "2022-09-04 13:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "AMAZÔNIA EM PÉ • GREENPEACE"}),
        this.eventDefault({date_start: "2022-09-04 14:00:00", date_final: false, place: {id:"espaco-viralata"}, fullDay: false, name: "OFICINA TERRAL E JARDIM PARA TODOS: COMO PLANTAR E CUIDAR DE SEU CACTO E SUCULENTA"}),
        
        this.eventDefault({date_start: "2022-09-04 07:00:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "SAMUEL MEDINA - CONTAÇÃO DE HISTÓRIA: DIVERSITÓRIAS"}),
        this.eventDefault({date_start: "2022-09-04 07:40:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "SAMUEL MEDINA - LANÇAMENTO DO LIVRO: UMA VISITA INESPERADA"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "RITA MAIA - INTERVENÇÃO LITERÁRIA - LIVRO: OBJETO DESEJO"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "LU FONSECA - LANÇAMENTO DE LIVROS"}),
        this.eventDefault({date_start: "2022-09-04 11:00:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "LEINER HOKI - QUEM VAI ME DAR UM BUQUÊ DE ROSAS"}),
        this.eventDefault({date_start: "2022-09-04 11:30:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "IZA REYS - LANÇAMENTO DO LIVRO: CAMINHO DE VOLTA PRA CASA"}),
        this.eventDefault({date_start: "2022-09-04 14:00:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "MOB COLETIVO - É SÓ UMA CARTA DE AMOR"}),
        this.eventDefault({date_start: "2022-09-04 15:30:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "ELIANA MARIA DE OLIVEIRA SÁ - LANÇAMENTO DO LIVRO “QUASE UMA CONFISSÃO”"}),
        this.eventDefault({date_start: "2022-09-04 17:00:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "CONCEIÇÃO AUXILIADORA DE OLIVEIRA - POESIA EM TRÂNSITO"}),
        this.eventDefault({date_start: "2022-09-04 18:00:00", date_final: false, place: {id:"arcos-literatura"}, fullDay: false, name: "TATIANE MOREIRA FERREIRA - SARAU FILHAS DA TERRA"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "AZULA QUEEN QUARTET (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-03 20:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "PLANB (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-03 21:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "TIOCAPONE (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-03 22:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "PEPOUS PEOPLE (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-03 23:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "GRAMA HERO (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-04 00:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "TREM DOIDO (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-04 01:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "MEGGERA (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-04 02:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "TRIBAL LEGACY (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-04 03:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "DESISTÊNCIA ZERO (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-04 04:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "MORTO (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-04 05:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "FRESH BLOOD (BH Stone)"}),
        this.eventDefault({date_start: "2022-09-04 06:10:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "SÉRGIO DIAZ E BANDA (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 07:40:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "BRONX (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 09:10:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "COALLIZZÃO (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 10:40:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "MC NENÊ (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 12:00:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "GUIMA DO ZILAH (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 13:20:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "DJ VITIN DO PC (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 14:50:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "DJ NATTAN (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 16:10:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "OREIA (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 17:40:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "XENON (Fora de Cena)"}),
        this.eventDefault({date_start: "2022-09-04 19:10:00", date_final: false, place: {id:"palco-viaduto"}, fullDay: false, name: "MONGE MC - SHOW DE 10 ANOS DO EP CAMINHODEZION VOL.I"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "SILAS PRADO SEXTETO"}),
        this.eventDefault({date_start: "2022-09-03 20:20:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "JENNIFER SOUZA - “PACÍFICA PEDRA BRANCA”"}),
        this.eventDefault({date_start: "2022-09-03 21:40:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "JÚLIA TIZUMBA - “SHOW MINÊRA”"}),
        this.eventDefault({date_start: "2022-09-03 23:25:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "DUO MITRE - “SEIVA”"}),
        this.eventDefault({date_start: "2022-09-04 00:45:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "TUTU COM TACACÁ - “CARIMBÓ PARAENSE COM JEITINHO MINEIRO”"}),
        this.eventDefault({date_start: "2022-09-04 02:15:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "SEU VIZINHO - “TODOMUNDOJUNTOEAGLOMERADO”"}),
        this.eventDefault({date_start: "2022-09-04 04:15:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "BLOCO FUNK YOU"}),
        this.eventDefault({date_start: "2022-09-04 06:00:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "KEYROGA E BANDA KALIMBA"}),
        this.eventDefault({date_start: "2022-09-04 08:25:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "LIVIA ITABORAHY - SERENATA"}),
        this.eventDefault({date_start: "2022-09-04 09:55:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "DUO RETRATOS DA CANÇÃO - “LENDAS E CANTOS AMAZÔNICOS”"}),
        this.eventDefault({date_start: "2022-09-04 11:15:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "BANDA DE MÚSICA DA GUARDA MUNICIPAL"}),
        this.eventDefault({date_start: "2022-09-04 12:45:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "CANTATA 2022 - 10 ANOS EM CANTO - ALUNOS DAS ESCOLAS MUNICIPAIS DE BH (SMED)"}),
        this.eventDefault({date_start: "2022-09-04 14:00:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "PERFORMANCE POÉTICA DE NÍVEA SABINO COM PIETA POETA E PEDRO BOMBA (Dia da Amazônia)"}),
        this.eventDefault({date_start: "2022-09-04 14:20:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "NATH RODRIGUES (Dia da Amazônia)"}),
        this.eventDefault({date_start: "2022-09-04 15:10:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "INTERVENÇÕES KDU DOS ANJOS, TEFFY DJ E FAVELINHA DANCE (Dia da Amazônia)"}),
        this.eventDefault({date_start: "2022-09-04 15:30:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "KAÊ GUAJAJARA (Dia da Amazônia)"}),
        this.eventDefault({date_start: "2022-09-04 16:50:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "VERONEZ CONVIDA SÉRGIO PERERÊ E CORAL (Dia da Amazônia)"}),
        this.eventDefault({date_start: "2022-09-04 18:00:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "FERNANDA TAKAI (Dia da Amazônia)"}),
        this.eventDefault({date_start: "2022-09-04 19:10:00", date_final: false, place: {id:"parque-municipal-palco-gramado"}, fullDay: false, name: "SWING SAFADO (Dia da Amazônia)"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "ISABEL CASIMIRO - TOADAS DE REINADO NA VOZ DA RAINHA"}),
        this.eventDefault({date_start: "2022-09-03 21:30:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "MONSTRA - FESTIVAL DANÇA DE SALÃO CONTEMPORÂNEA - CASA QUATRO - ME BREGA BAILE"}),
        this.eventDefault({date_start: "2022-09-03 23:00:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "COLADERA - SHOW"}),
        this.eventDefault({date_start: "2022-09-04 01:00:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "CHRONUS - O ESPETÁCULO DRAG"}),
        this.eventDefault({date_start: "2022-09-04 02:30:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "CABARÉ DAS DIVINAS TETAS"}),
        this.eventDefault({date_start: "2022-09-04 04:30:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "VOGUE FEVER"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "O MONSTRO DO LIXO - CIA. CANDONGAS E OUTRAS FIRULAS"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "O MENINO SABINO - CIA. CANTA CONTOS"}),
        this.eventDefault({date_start: "2022-09-04 10:10:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "MUSICAL SAMBA DO ARNESTO - GRUPO ARTÍSTICO DA APAE-BH"}),
        this.eventDefault({date_start: "2022-09-04 11:10:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "ESPETÁCULO DE MARIONETES - CATIN NARDI - TEATRO NAVEGANTE"}),
        this.eventDefault({date_start: "2022-09-04 12:20:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "OS BAIANINHAS - AXÉ E OZADIA EM VERSÃO MIRIM"}),
        this.eventDefault({date_start: "2022-09-04 13:35:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "HISTÓRIAS SOBRE SAPAS E SAPATOS"}),
        this.eventDefault({date_start: "2022-09-04 14:40:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "RESIDÊNCIA LIQUIDIFICADOR"}),
        this.eventDefault({date_start: "2022-09-04 15:40:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "PEDRO MORAIS - “AGORA”"}),
        this.eventDefault({date_start: "2022-09-04 17:10:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "GABRIELA VIEGAS (Verbo Gentileza+Rolê)"}),
        this.eventDefault({date_start: "2022-09-04 18:40:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "LUIZA BRINA (Verbo Gentileza+Rolê)"}),
        this.eventDefault({date_start: "2022-09-04 19:55:00", date_final: false, place: {id:"parque-municipal-palco-parque"}, fullDay: false, name: "19H55 (Verbo Gentileza+Rolê)"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"INTERVENÇÕES DE LED PELO PARQUE"}, fullDay: true, name: "DUAS IDEIAS"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque"}, fullDay: true, name: "TRANS/PARENTES - EFE GODOY"}),
        this.eventDefault({date_start: "2022-09-03 21:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PROJEÇÕES NAS ÁRVORES PRÓXIMAS A ENTRADA A AFONSO PENA"}, fullDay: false, name: "NATUREZA VIVA - DEISE OLIVEIRA CONVIDA THIAGO MIOTTO"}),
        this.eventDefault({date_start: "2022-09-03 22:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA DOS PATINS"}, fullDay: false, name: "THE FLOW DANÇAS URBANAS - BATALHA NA VIRADA"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ALAMEDA DOS MARRECOS"}, fullDay: false, name: "BOTÂNICA URBANA - BANQUETE BOTÂNICO"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ALAMEDA DOS MARRECOS"}, fullDay: false, name: "MUNDO ECOS - COMPOSTAGEM É VIDA!"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ALAMEDA DOS MARRECOS"}, fullDay: false, name: "VERBO GENTILEZA + ROLÉ - AGROECOLOGIA E PRODUTORES LOCAIS"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA FICUS"}, fullDay: false, name: "ESCOLA LIVRE DE ARTES ARENA DA CULTURA - SARAU VAGABUNDO DE TODO MUNDO - POÉTICAS DO REENCONTRO"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "OS CAMINHOS DE PACHAMAMA - EDIÇÃO BH É TERRA INDIGENA - COMITÊ MINEIRO DE APOIO À CAUSA INDÍGENA"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO ESPAÇO CINE PARQUE"}, fullDay: false, name: "HIGHLINE FEELINGS - SLACKLINE PARA TODOS"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PALCO GRAMADO"}, fullDay: false, name: "OFICINA MALABARES PARA INICIANTES COM GUTO FERREIRA"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ALAMEDA DOS MARRECOS"}, fullDay: false, name: "BIOFÁBRICA: FÁBRICA DE JOANINHAS - SECRETARIA MUNICIPAL DE MEIO AMBIENTE"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "UMA PERDA SÚBITA DE FLORES - CIA. DE DANÇA DO PALÁCIO DAS ARTES - FUNDAÇÃO CLÓVIS SALGADO"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ESPAÇO CINE PARQUE"}, fullDay: false, name: "VERBO GENTILEZA + ROLÉ - YOGA CANTADA COM FLÁVIA FERRAZ"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "RUA DE BRINCAR - MUSEU DE BRINQUEDOS - ArcelorMittal"}),
        this.eventDefault({date_start: "2022-09-04 11:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ESPAÇO CINE PARQUE"}, fullDay: false, name: "VERBO GENTILEZA + ROLÉ - RENATO MOURA COM GONGO"}),
        this.eventDefault({date_start: "2022-09-04 11:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA DOS PATINS"}, fullDay: false, name: "CIA CIRCUNSTÂNCIA - CIRCO DE FAMÍLIA"}),
        this.eventDefault({date_start: "2022-09-04 11:30:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "(IN)TENSÕES - CIA. DE DANÇA DO PALÁCIO DAS ARTES - FCS"}),
        this.eventDefault({date_start: "2022-09-04 11:30:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA FICUS"}, fullDay: false, name: "SLAM TODOS ESTÃO SURDOS"}),
        this.eventDefault({date_start: "2022-09-04 12:15:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PALCO GRAMADO"}, fullDay: false, name: "NA PRACINHA - OFICINA DE VARINHAS DE IMAGINAR"}),
        this.eventDefault({date_start: "2022-09-04 13:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "ESQUETE \"ANDE PREVENIDO\" - BHTRANS"}),
        this.eventDefault({date_start: "2022-09-04 13:30:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA DOS PATINS"}, fullDay: false, name: "BLOCO MAGNÓLIA - OFICINA UM CORPO CORTEJO ENFEITADO PARA O JAZZ"}),
        this.eventDefault({date_start: "2022-09-04 13:30:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA FICUS"}, fullDay: false, name: "JANETE MARIA FERREIRA - SARAU LITERÁRIO"}),
        this.eventDefault({date_start: "2022-09-04 14:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PALCO GRAMADO"}, fullDay: false, name: "BAMBOLÍRICAS - ENCONTRO DE BAMBOLÊS NA VIRADA"}),
        this.eventDefault({date_start: "2022-09-04 14:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "ESQUETE “(DES)EMBARQUE”- BHTRANS"}),
        this.eventDefault({date_start: "2022-09-04 15:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA FICUS"}, fullDay: false, name: "SLAM CLUBE DA LUTA"}),
        this.eventDefault({date_start: "2022-09-04 15:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ESPAÇO CINE PARQUE"}, fullDay: false, name: "VERBO GENTILEZA + ROLÉ - RODA DE CONVERSA SOBRE GASTRONOMIA COM FELIPE RAMEH E ORLANDO JUNIOR"}),
        this.eventDefault({date_start: "2022-09-04 15:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA DOS PATINS"}, fullDay: false, name: "OFICINA DE HIP-HOP - FÁBRICA DE GRAFFITI - ArcelorMittal"}),
        this.eventDefault({date_start: "2022-09-04 15:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "ESQUETE “LIGAÇÃO INTERROMPIDA” - BHTRANS"}),
        this.eventDefault({date_start: "2022-09-04 15:30:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"ENTRADA DA ANDRADAS SENTIDO ESPAÇO CINE PARQUE"}, fullDay: false, name: "BATUQUE SALUBRE - ARAUTOS DO GUETO - INSTITUTO UNIMED-BH"}),
        this.eventDefault({date_start: "2022-09-04 15:30:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "GRUPO INTERNACIONAL MUNDO CAPOEIRA GINGUETO"}),
        this.eventDefault({date_start: "2022-09-04 16:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRÓXIMO AO PARQUINHO"}, fullDay: false, name: "ESQUETE “DOIS LADOS” - BHTRANS"}),
        this.eventDefault({date_start: "2022-09-04 16:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA DO TRENZINHO"}, fullDay: false, name: "CAMILO GAN - CORPO ORALIDADE"}),
        this.eventDefault({date_start: "2022-09-04 16:00:00", date_final: false, place: {id:"parque-municipal-circuito-parque", name:"PRAÇA DOS PATINS"}, fullDay: false, name: "AS PANDERISTAS - RODA DE PANDEIRO"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "RAP, O CANTO DA CEILÂNDIA (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-03 19:30:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "DIAS DE GREVE (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-03 20:05:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "ABDUÇÃO (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-03 20:55:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "ENTRE NÓS E O MUNDO (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-03 21:30:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "FILME DE RUA (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-03 22:09:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "MEMÓRIAS DE MIM (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-03 22:40:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "DUELO DE MC’S NACIONAL DE 2013 (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-03 23:45:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "TRAVESSIA (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 00:05:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "RAPSÓDIA PARA UM HOMEM NEGRO (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 00:45:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "NOIR BLUE, DESLOCAMENTOS DE UMA DANÇA (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 01:25:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "BH TEM HIP HOP (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 03:20:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "CLIPES BRO MC’S (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 03:45:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "ENCONTRO DE PAJÉS (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 04:25:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "MÃTÃNÃG, A ENCANTADA (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 04:55:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "ATL 2017 (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 05:15:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "WHASÉ DARASE / TRABALHO DA ROÇA (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 05:50:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "A ORIGEM DA ALMA - TEKOWE NHEPYRUN (Cine Quintal Ocupa)"}),
        this.eventDefault({date_start: "2022-09-04 16:00:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "SOMOS COMUNIDADE - NÃO HÁ SOL A SÓS - INSTITUTO UNIMED-BH"}),
        this.eventDefault({date_start: "2022-09-04 18:00:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "VERBO GENTILEZA + ROLÉ - A GENTE LUTA MAS COME FRUTA"}),
        this.eventDefault({date_start: "2022-09-04 18:55:00", date_final: false, place: {id:"parque-municipal-cine-parque"}, fullDay: false, name: "VERBO GENTILEZA + ROLÉ - SESSÃO COMENTADA DO FILME “A GENTE LUTA MAS COME FRUTA” COM DANY AMARAL E CAROL BRAGA"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"rua-tamoios-lateral-parque"}, fullDay: true, name: "ESTÚDIO LUPA - CAÇA PALAVRAS DO FUTURO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {name:"AV. ANDRADAS, EMBAIXO DO VIADUTO SANTA TEREZA"}, fullDay: true, name: "GRUPO VIELA - ZONA DE AFETO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {name:"TÚNEL ESTAÇÃO CENTRAL"}, fullDay: true, name: "PORTACOPO PRÁTICAS DE ARQUITETURA - PRISMA"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"rua-aarao-reis"}, fullDay: true, name: "QUANDO COLETIVO - ATÉ QUANDO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"praca-rui-barbosa"}, fullDay: true, name: "4a EDIÇÃO DA MOSTRA DE ARTE LÉSBICA DE BH"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {name:"EZEQUIEL DIAS - FACHADA DA FACULDADE DE CIÊNCIAS MÉDICAS"}, fullDay: false, name: "MOSTRA DE CURTAS DE CINEASTAS E ANIMADORES DE BH - TEATRO FELUMA - FUNDAÇÃO EDUCACIONAL LUCAS MACHADO"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"avenida-andradas-367"}, fullDay: false, name: "LABIRINTO REDUÇÃO DE DANOS (SECRETARIA MUNICIPAL DE SAÚDE)"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"avenida-andradas-367"}, fullDay: false, name: "LABIRINTO CONSULTÓRIO DE RUA (SECRETARIA MUNICIPAL DE SAÚDE)"}),
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {name:"EDIFÍCIO DUQUE DE CAXIAS - RUA DA BAHIA COM VIADUTO"}, fullDay: false, name: "EDIFÍCIO PÍXEL - RIBEIRO & CARVALHO)"}),
        this.eventDefault({date_start: "2022-09-03 20:00:00", date_final: false, place: {name:"PISTA DE SKATE DEBAIXO DO VIADUTO SANTA TEREZA"}, fullDay: false, name: "BAILE UAI SOUND SYSTEM"}),
        this.eventDefault({date_start: "2022-09-03 20:00:00", date_final: false, place: {name:"VISÍVEL DOS ARCOS DO VIADUTO"}, fullDay: false, name: "ANANDACOLAA - PROJEÇÃO “PRETO PRESENTE”"}),
        this.eventDefault({date_start: "2022-09-03 22:00:00", date_final: false, place: {id:"praca-rui-barbosa"}, fullDay: false, name: "BLOCO FÚNEBRE 10 ANOS"}),
        this.eventDefault({date_start: "2022-09-03 22:00:00", date_final: false, place: {name:"CIRCULAÇÃO PELO HIPER CENTRO"}, fullDay: false, name: "ED MARTE DA CASA-MÓVEL-DO-AMOR"}),
        this.eventDefault({date_start: "2022-09-03 22:00:00", date_final: false, place: {name:"VISÍVEL DOS ARCOS DO VIADUTO"}, fullDay: false, name: "SILVI CLAPP E VJ FLAME - PROJEÇÃO “AS RUAS FALAM”"}),
        this.eventDefault({date_start: "2022-09-04 07:00:00", date_final: false, place: {id:"praca-rui-barbosa"}, fullDay: false, name: "INSTALAÇÃO AGÔ AGÔ - JOACÉLIO BATISTA E MARCEL DIOGO"}),
        this.eventDefault({date_start: "2022-09-04 08:00:00", date_final: false, place: {id:"rua-tamoios-lateral-parque"}, fullDay: false, name: "ATELIÊ NA RUA - WANATTA RODRIGUES E GUTO MARTINS"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {name:"EM FRENTE CINE TEATRO BRASIL VALOUREC"}, fullDay: false, name: "BH AO PÉ DO OUVIDO"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"avenida-andradas-367"}, fullDay: false, name: "LABIRINTO REDUÇÃO DE DANOS (SECRETARIA MUNICIPAL DE SAÚDE)"}),
        this.eventDefault({date_start: "2022-09-04 09:00:00", date_final: false, place: {id:"avenida-andradas-367"}, fullDay: false, name: "LABIRINTO CONSULTÓRIO DE RUA (SECRETARIA MUNICIPAL DE SAÚDE)"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {name:"AVENIDA DOS ANDRADAS"}, fullDay: false, name: "ENCONTRO DE OPALAS"}),
        this.eventDefault({date_start: "2022-09-04 10:00:00", date_final: false, place: {id:"rua-tamoios-lateral-parque"}, fullDay: false, name: "GALLA ONFIRE - “ZONA AUTÔNOMA”"}),
        this.eventDefault({date_start: "2022-09-04 12:00:00", date_final: false, place: {name:"RUA DOS TAMÓIOS - DEBAIXO DO VIADUTO - PISTA DE SKATE"}, fullDay: false, name: "EU AMO DISCO - PISTA DE PATINAÇÃO DANÇANTE"}),
        this.eventDefault({date_start: "2022-09-04 14:00:00", date_final: false, place: {id:"rua-aarao-reis"}, fullDay: false, name: "RENFA: REDE NACIONAL DE FEMINISTAS ANTIPROIBICIONISTAS - TENDA DE REDUÇÃO DE DANOS DAS MANAS, MINAS E MONAS"}),
        this.eventDefault({date_start: "2022-09-04 14:30:00", date_final: false, place: {name:"PORTARIA PRINCIPAL DO PARQUE MUNICIPAL NA AFONSO PENA"}, fullDay: false, name: "MARACATU LUA NOVA"}),
        this.eventDefault({date_start: "2022-09-04 16:00:00", date_final: false, place: {id:"rua-aarao-reis"}, fullDay: false, name: "KARAOKÊ MINAS SOLIDÁRIO - CAMPEONATO DE KARAOKÊ"}),
        this.eventDefault({date_start: "2022-09-04 18:00:00", date_final: false, place: {name:"PARQUE MUNICIPAL PRÓXIMO A SAÍDA DA ANDRADAS"}, fullDay: false, name: "BOI ROSADO - TRAVESSIA ILUMINADA NA VIRADA CULTURAL"}),
        this.eventDefault({date_start: "2022-09-04 18:00:00", date_final: false, place: {id:"avenida-andradas-367", name:"EDIFÍCIO CENTRAL - AV. DOS ANDRADAS, 367"}, fullDay: false, name: "BOI LIVRE - ESCOLA LIVRE DE ARTES ARENA DA CULTURA"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"escada-cine-theatro"}, fullDay: false, name: "BLOCO SAÚDE - INSTITUTO UNIMED-BH"}),
        this.eventDefault({date_start: "2022-09-03 20:30:00", date_final: false, place: {id:"escada-cine-theatro"}, fullDay: false, name: "BAILE BLACK - COMUNIDADE DO SOUL"}),
        this.eventDefault({date_start: "2022-09-03 22:00:00", date_final: false, place: {id:"escada-cine-theatro"}, fullDay: false, name: "SHOW RAP DA PAZ"}),
        this.eventDefault({date_start: "2022-09-03 23:30:00", date_final: false, place: {id:"escada-cine-theatro"}, fullDay: false, name: "TRIO OUVIRÁ"}),
        this.eventDefault({date_start: "2022-09-04 01:20:00", date_final: false, place: {id:"escada-cine-theatro"}, fullDay: false, name: "CHOROSAS - COMPOSITORAS NA RODA"}),
        this.eventDefault({date_start: "2022-09-04 16:00:00", date_final: false, place: {id:"escada-cine-theatro"}, fullDay: false, name: "SAMBA D'OURO NA VIRADA"}),
        
        this.eventDefault({date_start: "2022-09-03 19:00:00", date_final: false, place: {id:"espaco-forro"}, fullDay: false, name: "MONSTRA - FESTIVAL DE DANÇA DE SALÃO CONTEMPORÂNEA - LAURA JAMES - FORRÓ QUEER"}),
        this.eventDefault({date_start: "2022-09-03 22:00:00", date_final: false, place: {id:"espaco-forro"}, fullDay: false, name: "FORRÓ SOUND SYSTEM O AUTÊNTICO FORRÓ PÉ DE SERRA, COMANDADOS POR 15 DJ'S SELETORES E 10 PROFISSIONAIS DA DANÇA. PARA TODO MUNDO SE MISTURAR E CURTIR FAZENDO O BAILE ACONTECER."}),
        this.eventDefault({date_start: "2022-09-04 00:00:00", date_final: false, place: {id:"espaco-forro"}, fullDay: false, name: "FORRÓ SOUND SYSTEM O AUTÊNTICO FORRÓ PÉ DE SERRA, COMANDADOS POR 15 DJ'S SELETORES E 10 PROFISSIONAIS DA DANÇA. PARA TODO MUNDO SE MISTURAR E CURTIR FAZENDO O BAILE ACONTECER."}),
        
        this.eventDefault({
          date_start: "2022-09-04 10:00:00",
          date_final: "2022-09-04 18:00:00",
          place: {name:"BDMG CULTURAL - RUA BERNARDO GUIMARÃES, 1600, LOURDES"},
          fullDay: false,
          name: "BÁRBARA LISSA E MARIA VAZ - MOSTRA QUANDO O TEMPO DURA UMA TONELADA.",
        }),
        
        this.eventDefault({
          date_start: "2022-09-04 10:00:00",
          date_final: "2022-09-04 17:00:00",
          place: {name:"BIBLIOTECA PÚBLICA ESTADUAL DE MG - PRAÇA DA LIBERDADE, 21, SAVASSI"},
          fullDay: false,
          name: "VISITAÇÃO À EXPOSIÇÃO WANDER PIROLI: INVENTOR DO QUE EXISTE, NA GALERIA PAULO CAMPOS GUIMARÃES.",
        }),
        this.eventDefault({
          date_start: "2022-09-04 11:00:00",
          date_final: "2022-09-04 17:00:00",
          place: {name:"CENTRO DE ARTE POPULAR - PRAÇA DA LIBERDADE, 21, SAVASSI"},
          fullDay: false,
          name: "EXPOSIÇÃO PERMANENTE",
        }),
        this.eventDefault({
          date_start: "2022-09-03 19:00:00",
          date_final: "2022-09-03 00:00:00",
          place: {name:"CENTRO DE ATENDIMENTO AO TURISTA MERCADO DAS FLORES - AV. AFONSO PENA, 1055, CENTRO"},
          fullDay: false,
          name: "INSTALAÇÃO XIU, DE MARCUS DEUSDEDIT, COM CURADORIA DE WAGNER NARDY.",
        }),
        this.eventDefault({
          date_start: "2022-09-04 10:00:00",
          date_final: "2022-09-04 18:00:00",
          place: {name:"CENTRO DE ATENDIMENTO AO TURISTA MERCADO DAS FLORES - AV. AFONSO PENA, 1055, CENTRO"},
          fullDay: false,
          name: "INSTALAÇÃO XIU, DE MARCUS DEUSDEDIT, COM CURADORIA DE WAGNER NARDY.",
        }),
        this.eventDefault({
          date_start: "2022-09-03 10:00:00",
          date_final: "2022-09-03 22:00:00",
          place: {name:"CENTRO CULTURAL BANCO DO BRASIL - PRAÇA DA LIBERDADE, 450, FUNCIONÁRIOS"},
          fullDay: false,
          name: "EXPOSIÇÃO BRASILIDADE PÓS-MODERNISMO. 20H • TEATRO: ENQUANTO ESTAMOS AQUI.",
        }),
        this.eventDefault({
          date_start: "2022-09-04 10:00:00",
          date_final: "2022-09-04 22:00:00",
          place: {name:"CENTRO CULTURAL BANCO DO BRASIL - PRAÇA DA LIBERDADE, 450, FUNCIONÁRIOS"},
          fullDay: false,
          name: "EXPOSIÇÃO BRASILIDADE PÓS-MODERNISMO. 20H • TEATRO: ENQUANTO ESTAMOS AQUI.",
        }),
      ],
    };
  },
  methods: {
    placeDefault(data = {}) {
      return {
        name: "No name",
        ...data
      };
    },
    placeById(id, def=false) {
      return this.places.filter(item => item.id==id)[0] || def;
    },
    eventDefault(data = {}) {
      return {
        datetime: "2022-09-03 19:00:00",
        fullDay: false,
        name: "No name",
        price: 0,
        place: {coords:[-19.912998, -43.940933]},
        ...data
      };
    },
    mapCenterSet(coords) {
      this.mapBind.center = coords;
    },
  },
  computed: {
    eventsWithPlaces() {
      return this.events.map(item => {
        item = JSON.parse(JSON.stringify(item));

        if (item.place.id) {
          const place = this.places.filter(place => place.id==item.place.id);
          item.place = place[0] || this.placeDefault();
        }
        
        return item;
      });
    },
    placesWithEvents() {
      let places = this.places.map(place => {
        place = JSON.parse(JSON.stringify(place));
        place.events = this.events.filter(item => item.place.id == place.id).map(item => {
          item.place = this.placeById(item.place.id);
          return item;
        });
        return place;
      });


      let others = this.placeDefault({name:"Outros eventos", coords:[-19.912998, -43.940933], events:[]});

      this.events.forEach(evt => {
        if (!evt.place.id) {
          evt.place = this.placeDefault(evt.place);
          others.events.push(evt);
        }
      });

      places.push(others);
      return places;
    },
  },
  mounted() {
    setTimeout(() => {
      this.$el.querySelectorAll('.scroll-bottom').forEach(elem => {
        elem.scrollTop = elem.scrollHeight;
      });
    }, 200);
  },
}
</script>
