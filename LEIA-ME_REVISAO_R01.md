# MODULE RELAY PTH — Revisão R01 — 2026-11-12
Zat Electronic · KiCad 10.0 · padrão Zat (doc 11)

## Arquivos
- "MODULE RELAY.*" -> MODULE_RELAY_PTH.* (sem espaços).
- .kicad_dru com uma regra (pedida pelo Kenneth): GND a 3 mm de COMUM / NO / NC (contatos do relé).
- Removidos: .history, fp-info-cache, ERC.rpt, DRC.rpt, archive_3d_models.log.
- Removidos: SCHEMATIC.jpg, "LAYOUT PCB.jpg" e "PCB 3D MODEL.jpg". Mostravam a numeração antiga e o README não os usa (usa imagem_1/2.png).

## Esquema
- Esquema plano -> capa A2 + 2 folhas: 02 RELÉ (opto + driver + relé), 03 CONEXÕES (J1 / J2 + PWR_FLAG).
- Reanotação como na versão SMD: o LED L1 virou D1 (prefixo de LED). Diodo D1 -> D2, R3 -> R2, R4 -> R3, R2 -> R4.
  U1, Q1, K1, J1, J2, R1 continuam iguais.
- J1/J2: ZAT_Connector:Screw_Terminal_01x03 + ZAT_TerminalBlock 03P DG306 (3D DG306). Os pinos ficam nos mesmos pontos.
- Footprints ZAT (cópias exatas do KiCad + 3D em ${ZAT_3D}):

  | Ref | Footprint | 3D |
  |-----|-----------|----|
  | U1 | ZAT_Package_DIP:DIP-4_W7.62mm_LongPads_PC817 | PC817/PC817_DIP.step |
  | Q1 | ZAT_Package_TO_SOT_THT:TO-92_HandSolder_BC548 | TRANSISTORES/Transistor BC548.STEP |
  | K1 | ZAT_Relay_THT:Relay_SPDT_SANYOU_SRD_Series_Form_C_AY1RC2 | RELE/RELÉ AY1RC2 12VDC 15A.STEP |
  | D2 | ZAT_Diode_THT:..._1N4007 | (existente) |
  | D1 | ZAT_LED:LED_D5.0mm_Blue | (existente) |
  | R1..R4 | ZAT_Resistor_THT:R_Axial_DIN0204_..._220R / 4K7 / 470R / 10K | RESISTORES/... Value xx.STEP |

- PWR_FLAG em GND e +12V. Valores normalizados (220R, 4k7, 10k, 470R). Nenhuma severidade em "ignore".

## PCB (cobre não alterado: nenhum pad nem trilha mudou)
- Furos -> H1..H4, "Not in schematic".
- Logos: courtyard real + "Not in schematic". Os desenhos de parafuso foram afastados 1,6-1,74 mm dos furos.
- Referências visíveis em F.SilkS 1,0 mm.
- Zona GND sem preenchimento salvo: preencher com B. Na simulação, todo o GND fica num só grupo.

## Biblioteca global (já gravada no PC, md5 conferido)
- footprints/ZAT_Package_DIP.pretty (nova): DIP-4_W7.62mm_LongPads_PC817.
- footprints/ZAT_Package_TO_SOT_THT.pretty (nova): TO-92_HandSolder_BC548.
- footprints/ZAT_Resistor_THT.pretty: + R_Axial_DIN0204_L3.6mm_D1.6mm_P7.62mm_Horizontal_4K7.
- fp-lib-table: + ZAT_Package_DIP, + ZAT_Package_TO_SOT_THT.

## README
- Conferido contra o circuito:
  - diagrama refeito;
  - BOM com a nova numeração;
  - J2 = NO / COMUM / NC (como na placa);
  - tabela de diferenças com a versão SMD atualizada (LTV-357T, MMBT2222A, S1M);
  - estrutura de arquivos atualizada.
- Retirada a afirmação de "isolação galvânica total" (ver abaixo).

## Pontos de projeto
- IMPORTANTE: NÃO há isolação galvânica.
  - O LED do opto (pino 2) volta para o mesmo GND do borne J1 que alimenta a bobina.
  - A serigrafia "ISOLATED MODULE RELAY" continua na placa (não alterada) e promete isolação que não existe.
  - Para isolar de verdade é preciso um borne separado para o GND da entrada, o que exige mudar o layout.
- RESOLVIDO: a zona GND passava a 1 mm das trilhas dos contatos (COMUM / NO / NC).
  - Regra "REDE_AC_GND_3mm" no .kicad_dru: 3 mm só entre GND e essas 3 nets (resto da placa igual, cobre não movido).
  - Simulação do preenchimento: nenhum pad/trilha GND a menos de 3 mm dos contatos; todo o GND continua num só grupo.
  - Conferir a creepage exigida pela norma da aplicação final.
- MELHORIA: R3 470R dá ~19 mA no LED azul de 5 mm (perto do máximo de 20 mA). Com 1k fica em ~9 mA.
- OK: o BC548 suporta 100 mA e a bobina consome ~30-40 mA. R1 220R dá ~17 mA no LED do opto com 5 V e ~9 mA com 3,3 V.

## Após abrir no KiCad
1. Reiniciar o KiCad (tabela de bibliotecas atualizada).
2. ERC no esquema.
3. PCB: B (preencher zonas) -> F8 (deve vir sem alterações) -> DRC.
