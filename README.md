<div align="center">

<img src="imagem_1.png" alt="MODULE RELAY — Vista Superior" width="800"/>

# MODULE RELAY

**Módulo de relé com acionamento por nível alto (High Level Trigger), componentes totalmente através-furo (PTH), optoacoplador PC817 e relé de potência 12VDC / 15A**

[![KiCad](https://img.shields.io/badge/KiCad-10-blue?logo=kicad&logoColor=white)](https://www.kicad.org/)
[![Relé](https://img.shields.io/badge/Rel%C3%A9-12VDC%2015A-darkred)](.)
[![Isolação](https://img.shields.io/badge/Isola%C3%A7%C3%A3o-%C3%93ptica%20PC817-orange)](.)
[![Trigger](https://img.shields.io/badge/Trigger-High%20Level-green)](.)
[![Montagem](https://img.shields.io/badge/Montagem-PTH-blueviolet)](.)
[![ZAT ELECTRONIC](https://img.shields.io/badge/Feito%20por-ZAT%20ELECTRONIC-black)](.)
[![Made in Brazil](https://img.shields.io/badge/Made%20in-Brazil%20%F0%9F%87%A7%F0%9F%87%B7-009c3b)](.)

</div>

---

## 📋 Índice

- [MODULE RELAY](#module-relay)
  - [📋 Índice](#-índice)
  - [Visão Geral](#visão-geral)
  - [Imagens do Projeto](#imagens-do-projeto)
  - [Diferenças em relação ao MODULE RELAY SMD](#diferenças-em-relação-ao-module-relay-smd)
  - [Funcionalidades](#funcionalidades)
  - [Diagrama de Funcionamento](#diagrama-de-funcionamento)
  - [Especificações Técnicas](#especificações-técnicas)
  - [Lista de Materiais](#lista-de-materiais)
  - [Pinagem dos Conectores](#pinagem-dos-conectores)
    - [J1 — Entrada (Controle)](#j1--entrada-controle)
    - [J2 — Saída (Carga)](#j2--saída-carga)
  - [Aplicações](#aplicações)
  - [Estrutura do Repositório](#estrutura-do-repositório)
  - [Como Usar](#como-usar)
    - [Conexão básica com Arduino / ESP32](#conexão-básica-com-arduino--esp32)
    - [Exemplo de código Arduino](#exemplo-de-código-arduino)
    - [Dica de Montagem](#dica-de-montagem)
  - [⚠️ Avisos de Segurança](#️-avisos-de-segurança)
  - [Sobre](#sobre)

---

## Visão Geral

**MODULE RELAY** é um módulo de acionamento de relé com **acionamento por optoacoplador** (a entrada +IN e a bobina usam o mesmo GND do borne J1: não há isolação galvânica entre controle e alimentação; os contatos do relé são isolados da bobina), projetado pela **ZAT ELECTRONIC** utilizando **KiCad 10**. Diferente da versão SMD, esta placa utiliza exclusivamente **componentes através-furo (PTH)**, tornando-a ideal para montagem manual, prototipagem e laboratórios maker.

O circuito utiliza o optoacoplador **PC817** (DIP-4 PTH) para acoplar o sinal de controle (proveniente de microcontroladores como Arduino, ESP32, etc.) do circuito de potência. O transistor **BC548** (TO-92 PTH) aciona a bobina do relé de potência 12VDC, capaz de comutar cargas de até **15A em 125VAC ou 24VDC**.

> ⚡ **High Level Trigger** — o relé é acionado com sinal lógico alto (+3,3V ou +5V) no pino de entrada, com o LED do optoacoplador como carga do pino do microcontrolador.

---

## Imagens do Projeto

<div align="center">

<img src="imagem_1.png" alt="Vista Superior 3D" width="700"/>

*Vista superior — relé de potência, optoacoplador PC817 DIP, transistor BC548 e bornes KRE*

<br/>

<img src="imagem_2.png" alt="Vista Isométrica 3D" width="700"/>

*Vista isométrica — componentes PTH, LED azul 5mm e layout geral da placa*

<br/>



<br/>



<br/>



</div>

---

## Diferenças em relação ao MODULE RELAY SMD

| Característica | MODULE RELAY (PTH) | MODULE RELAY SMD |
|----------------|-------------------|-----------------|
| **Tipo de montagem** | Através-furo (PTH) | Montagem superficial (SMD) |
| **Optoacoplador** | PC817 DIP-4 PTH | LTV-357T SOP-4 SMD |
| **Transistor driver** | BC548 (TO-92 PTH) | MMBT2222A (SOT-23 SMD) |
| **Resistores** | Axial 0,5W PTH | SMD 0805 |
| **LED de status** | 5mm PTH azul | SMD 0805 |
| **Diodo de roda livre** | 1N4007 PTH axial | S1M SMA SMD |
| **Facilidade de montagem** | Alta — soldagem manual simples | Requer soldagem SMD |
| **Público alvo** | Iniciantes, makers, laboratório | Produção, compacto, profissional |

---

## Funcionalidades

- ✅ **Relé de potência 12VDC / 15A** — contatos SPDT (NO, COMUM, NC), 15A 125VAC / 15A 24VDC
- ✅ **Optoacoplador PC817** (DIP-4 PTH) — aciona o driver; controle e bobina compartilham o GND
- ✅ **Transistor BC548** (TO-92 PTH) — driver NPN para acionamento da bobina
- ✅ **Diodo de roda livre 1N4007** (PTH axial) — proteção contra tensão reversa da bobina
- ✅ **LED azul 5mm PTH** — indicação visual de relé acionado
- ✅ **High Level Trigger** — compatível com 3,3V e 5V (Arduino, ESP32, Raspberry Pi, etc.)
- ✅ **Bornes KRE parafuso** (3 pinos, passo 5,0mm) — conexão robusta para entrada e saída
- ✅ **Todos os componentes PTH** — montagem manual fácil, ideal para prototipagem
- ✅ **Made in Brazil** — serigrafia na PCB

---

## Diagrama de Funcionamento

```
Microcontrolador / Sinal de Controle
        │
    +IN ●──[R1 220Ω]──► U1 PC817 (LED, pino 1) ── pino 2 ── GND
                               │ (acoplamento óptico)
    +12V ─────────────► U1 coletor (pino 4)
                        U1 emissor (pino 3) ──[R2 4,7kΩ]──┬──► Base Q1 BC548
                                                        [R4 10kΩ]
                                                          │
                                                         GND
    +12V ──┬──────────────┬─────────[R3 470Ω]──[D1 LED azul]──┐
       [Bobina K1]   [D2 1N4007] (roda livre)                 │
           └──────────────┴───────────────────────────────────┴──► Coletor Q1 (emissor no GND)

              Contatos do Relé (J2 — OUT)
         ┌────────────────────────────────┐
         │   NO  │  COMUM  │  NC          │
         └────────────────────────────────┘
          Carga: até 15A / 125VAC ou 24VDC
```

---

## Especificações Técnicas

| Parâmetro | Valor |
|-----------|-------|
| **Relé** | 12VDC / SPDT (Form C) |
| **Tensão da Bobina** | 12VDC |
| **Corrente máx. de carga (AC)** | 15A @ 125VAC |
| **Corrente máx. de carga (DC)** | 15A @ 24VDC |
| **Tipo de contato** | SPDT — NO, NC, COMUM |
| **Tensão de alimentação do módulo** | +12V |
| **Tensão de controle (sinal IN)** | 3,3V a 5V (High Level Trigger) |
| **Optoacoplador** | PC817 DIP-4 — GND comum com a bobina |
| **Transistor driver** | BC548 (TO-92, NPN) |
| **Diodo de proteção** | 1N4007 (PTH axial) |
| **LED de status** | 5mm PTH azul |
| **Resistores** | Axial 0,5W PTH |
| **Conectores** | Borne KRE parafuso 3 pinos, passo 5,0mm |
| **Ferramenta de Projeto** | KiCad 10 |
| **Tipo de montagem** | PTH — Através-furo |

---

## Lista de Materiais

| Ref | Componente | Valor / Parte | Encapsulamento |
|-----|-----------|--------------|----------------|
| K1 | Relé de Potência | AY1RC2 12VDC / 15A SPDT | PTH (pinagem SANYOU SRD) |
| U1 | Optoacoplador | PC817 | DIP-4 PTH |
| Q1 | Transistor NPN | BC548 | TO-92 PTH |
| D2 | Diodo de Roda Livre | 1N4007 | PTH Axial |
| D1 | LED de Status | LED 5mm Azul | PTH 5mm |
| R1 | Resistor de entrada (LED do opto) | 220Ω | Axial PTH |
| R2 | Resistor série da base | 4,7kΩ | Axial PTH |
| R4 | Resistor pull-down da base | 10kΩ | Axial PTH |
| R3 | Resistor do LED de status | 470Ω | Axial PTH |
| J1 | Borne de Entrada (Controle) | +12V, +IN, GND | KRE 3 pinos 5,0mm |
| J2 | Borne de Saída (Carga) | NO, COMUM, NC | KRE 3 pinos 5,0mm |

---

## Pinagem dos Conectores

### J1 — Entrada (Controle)

| Pino | Sinal | Descrição |
|------|-------|-----------|
| 1 | +12V | Alimentação da bobina do relé |
| 2 | +IN | Sinal de controle (3,3V–5V = relé ON) |
| 3 | GND | Terra comum |

### J2 — Saída (Carga)

| Pino | Sinal | Descrição |
|------|-------|-----------|
| 1 | NO | Normalmente aberto (fecha quando acionado) |
| 2 | COMUM | Terminal comum do relé |
| 3 | NC | Normalmente fechado (abre quando acionado) |

---

## Aplicações

- 🏠 **Automação residencial** — acionamento de lâmpadas, tomadas e ventiladores
- 🤖 **Projetos com Arduino e ESP32** — controle de cargas AC
- 🏫 **Ensino e prototipagem** — componentes PTH facilmente soldáveis e substituíveis
- 💡 **Controle de iluminação** — painéis de LED de alta potência e luminárias
- 🔌 **Comutação de cargas** — relé separa os contatos de carga da bobina (GND de controle e de alimentação é comum)
- 📡 **IoT e domótica** — integração com sistemas MQTT, Home Assistant, etc.

---

## Estrutura do Repositório

```
MODULE_RELAY_PTH/
├── MODULE_RELAY_PTH.kicad_pro    # Arquivo de projeto KiCad 10
├── MODULE_RELAY_PTH.kicad_sch    # Esquemático: capa A2 (índice das folhas)
├── RELAY.kicad_sch               # Folha 02: optoacoplador + driver + relé
├── CONN.kicad_sch                # Folha 03: bornes IN / OUT + PWR_FLAG
├── MODULE_RELAY_PTH.kicad_pcb    # Layout da PCB (KiCad 10)
├── MODULE_RELAY_PTH.kicad_prl    # Configurações locais
├── MODULE_RELAY_PTH.kicad_dru    # Regra: GND a 3 mm dos contatos do relé
├── Zat_TitleBlock.kicad_wks      # Title block ZAT ELECTRONIC
├── packages3D/                   # Modelos 3D arquivados (referência)
├── imagem_1.png                  # Render 3D superior
├── imagem_2.png                  # Render 3D isométrico
├── LEIA-ME_REVISAO_R01.md        # O que mudou na revisão R01
└── README.md
```

---

## Como Usar

### Conexão básica com Arduino / ESP32

```
Arduino / ESP32             MODULE RELAY
───────────────────         ─────────────────
GND              ────────►  J1 - GND
Pino digital     ────────►  J1 - +IN

Fonte 12VDC (+)  ────────►  J1 - +12V
Fonte 12VDC (-)  ────────►  J1 - GND

Carga AC/DC      ────────►  J2 - COMUM + NO (ou NC)
```

### Exemplo de código Arduino

```cpp
#define RELAY_PIN 7

void setup() {
  pinMode(RELAY_PIN, OUTPUT);
  digitalWrite(RELAY_PIN, LOW); // relé desligado na inicialização
}

void loop() {
  digitalWrite(RELAY_PIN, HIGH); // aciona o relé
  delay(1000);
  digitalWrite(RELAY_PIN, LOW);  // desaciona o relé
  delay(1000);
}
```

### Dica de Montagem

> 🔧 Por ser totalmente PTH, recomenda-se a seguinte ordem de soldagem: resistores primeiro, depois diodo, transistor BC548, optoacoplador PC817, LED, relé e por último os bornes KRE.

## ⚠️ Avisos de Segurança

> 🔴 **ATENÇÃO — TENSÕES PERIGOSAS**

- Este módulo pode comutar tensões de **rede elétrica (110V / 220V AC)**. Manuseie com extremo cuidado.
- **Nunca toque nos terminais J2 (OUT)** enquanto houver carga CA conectada e o circuito energizado.
- Utilize **caixa de proteção** adequada quando instalar em ambientes com acesso de pessoas.
- Respeite a **corrente máxima de 15A** nos contatos do relé.
- O optoacoplador **não isola** o GND do microcontrolador do GND do módulo (são comuns no J1) e **não substitui normas de segurança elétrica**.
- A zona GND fica a 3 mm das trilhas e pads dos contatos do relé (COMUM / NO / NC), por regra no MODULE_RELAY_PTH.kicad_dru. Conferir a creepage exigida pela norma da aplicação final.
- Projeto destinado a **profissionais e experimentadores experientes**.

---

## Sobre

<div align="center">

Projetado por **ZAT ELECTRONIC**

*MODULE RELAY — Made in Brazil 🇧🇷*

[![KiCad](https://img.shields.io/badge/Projetado%20com-KiCad%2010-blue)](https://www.kicad.org/)
[![Open Source Hardware](https://img.shields.io/badge/Open%20Source-Hardware-brightgreen)](https://www.oshwa.org/)

</div>>