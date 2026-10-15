# Nettverkssikkerhetslab

> 🚧 **Under arbeid.** Laben bygges i faser. Fase 1 av 8 er ferdig, se [Fremdrift](#fremdrift) for status.

Et lite bedriftsnettverk bygget i Cisco Packet Tracer, med fokus på segmentering og herding av enheter. Laben bygges i faser, og hver fase dokumenteres her etter hvert som den blir ferdig.

![Topologi](docs/topology.png)

## Mål

Designe et nettverk for et lite kontor der ansatte, administratorer og gjester deler den samme fysiske infrastrukturen, men holdes logisk adskilt. Gjester skal bare nå internett, ansatte skal nå felles tjenester, og bare administratorer skal kunne administrere nettverksenhetene.

## Topologi

| Enhet | Modell | Rolle |
|---|---|---|
| Router0 | Cisco 2911 | Gateway, ruting mellom VLAN, ACL |
| Switch0 | Cisco 2960 | Aksessvitsj, opplink til ruteren |
| Switch1 | Cisco 2960 | Aksessvitsj |
| Server0 | Server-PT | Interne tjenester (DHCP, web) |
| PC0 til PC5 | PC-PT | Sluttbrukere |

### Kabling

| Fra | Port | Til | Port |
|---|---|---|---|
| Router0 | G0/0 | Switch0 | G0/1 |
| Switch0 | G0/2 | Switch1 | G0/1 |
| PC0, PC1, PC2 | Fa0 | Switch0 | Fa0/1, Fa0/2, Fa0/3 |
| Server0 | Fa0 | Switch0 | Fa0/4 |
| PC3, PC4, PC5 | Fa0 | Switch1 | Fa0/1, Fa0/2, Fa0/3 |

### Planlagt adressering

| VLAN | Navn | Subnett | Gateway |
|---|---|---|---|
| 10 | Admin | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Ansatte | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Gjest | 192.168.30.0/24 | 192.168.30.1 |
| 99 | Administrasjon | 192.168.99.0/24 | 192.168.99.1 |

## Fremdrift

- [x] **Fase 1:** Topologi og kabling
- [ ] **Fase 2:** VLAN og trunking
- [ ] **Fase 3:** Router on a stick (ruting mellom VLAN)
- [ ] **Fase 4:** DHCP per VLAN
- [ ] **Fase 5:** Herding av enheter (SSH, passord, bannere)
- [ ] **Fase 6:** Tilgangslister (ACL)
- [ ] **Fase 7:** Portsikkerhet
- [ ] **Fase 8:** Testing og sluttrapport

## Fase 1: Topologi og kabling

Alle enhetene er koblet sammen med rette kobberkabler. Koblingene mellom svitsjene og sluttbrukerenhetene kommer opp med en gang. Koblingen til ruteren er nede foreløpig, fordi grensesnittene på en ruter er administrativt slått av som standard. Den blir slått på i fase 3, når undergrensesnittene konfigureres.

## Filer

| Fil | Innhold |
|---|---|
| `network-security-lab.pkt` | Packet Tracer-prosjektet (åpnes med Packet Tracer 9.0 eller nyere) |
| `configs/` | Kjørende konfigurasjoner eksportert fra hver enhet, legges til per fase |
| `docs/` | Skjermbilder og testresultater |

## Verktøy

Cisco Packet Tracer 9.0, Cisco IOS CLI
