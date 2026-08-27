# OBS Game Capture — pin e cadeia de custódia

## Origem oficial

- projeto: OBS Studio
- release: `32.2.2`
- tag anotado: `fc546137470c0f4a5f1493b6e7815545ee1b170b`
- commit apontado pelo tag: `ba2f32bdf791005443988a4955e963663e16b1ed`
- arquivo: `OBS-Studio-32.2.2-Windows-x64.zip`
- SHA-256 oficial do ZIP:
  `4D6E40E3AB155F56B30DE517380566A206D74B63CDF5AD49AA596924768F97E1`
- checkout de desenvolvimento:
  `E:\DevTools\GG-Stream\OBS-32.2.2\source`
- extração oficial:
  `E:\DevTools\GG-Stream\OBS-32.2.2\windows-x64`

## Binários preservados byte por byte

Todos foram extraídos do ZIP acima e tiveram assinatura Authenticode válida de
`OBS Project, LLC`.

| Arquivo | SHA-256 |
| --- | --- |
| `graphics-hook32.dll` | `566B095DD1DE495A3F0233CB08D75AB3E7D7B184C80E2FC23F23F22CA8558632` |
| `graphics-hook64.dll` | `49C0DDEAC72B130D4F8AE90510219949022C1F992ADB48D81A4972F2CD6C2585` |
| `inject-helper32.exe` | `226DA6B414470D17A4B4D368BB55916AB3922B1AE10BB2325EA627F63B1AEA71` |
| `inject-helper64.exe` | `A785AE14B5DEBAE83404942D5EF7A51C83A53C603D6F5A23162D7F52FF96D9FF` |
| `get-graphics-offsets32.exe` | `4627F12B8295B1EBAFD9909DFD0EAA46583E68E8976C8FEF76E64122FD2149B6` |
| `get-graphics-offsets64.exe` | `79ED6D2A983CC93A7AD6B96EB9D0FAE21871988A2823CCE11D4060ACE35753FB` |

## Decisão de interoperabilidade

`graphics-hook` e `inject-helper` podem ser usados sem modificação. Isso exige
reproduzir no processo host o ABI oficial `1.8.8`:

- gerar os offsets DXGI/D3D com o executável oficial da arquitetura do jogo;
- criar keepalive e named pipe antes da injeção;
- abrir e configurar `CaptureHook_HookInfo<PID>`;
- preservar eventos e mutexes nomeados pelo PID;
- sinalizar `CaptureHook_Initialize<PID>`;
- mapear `CaptureHook_Texture_<HWND>_<map_id>`;
- abrir o handle D3D11 legado publicado em `shtex_data::tex_handle`.

O código de coordenação fica em `gg-game-capture-host.exe`, processo separado
GPL. O motor NVENC/libdatachannel não incorpora nem liga código OBS. A fronteira
entre os processos contém somente comandos, estado e handle de textura GPU;
nenhum pixel cru atravessa IPC.

## Licença e distribuição

OBS Studio e o host derivado usam GPL-2.0-or-later. Antes de distribuir uma
build do GG Stream com estes componentes, incluir:

- o arquivo `COPYING` oficial, sem alteração;
- avisos de copyright e atribuição OBS;
- esta identificação exata de release/commit;
- acesso ou oferta válida do código-fonte correspondente, incluindo o código do
  `gg-game-capture-host.exe` e eventuais modificações GPL.

Não modificar os binários assinados nem apresentar o host GG como binário
oficial assinado pelo OBS Project.

