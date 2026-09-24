# Gravistrap

<p align="center">
  <img src="src/Gravistrap/logo.png" width="180" alt="Gravistrap Logo"/>
</p>

<p align="center">
  <b>Bloxstrap esinlenmeli, hafif ve şeffaf Roblox bootstrapper</b><br/>
  FastFlag • Mod • Çoklu İstemci • Legacy • Server Overlay
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-Windows-0078D6?style=flat-square&logo=windows"/>
  <img src="https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square&logo=dotnet"/>
  <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square"/>
</p>

---

**Gravistrap**, Roblox'u kendi üzerinden başlatan bir Windows bootstrapper'ıdır. Orijinal Bloxstrap mantığını korur, üzerine çoklu istemci, legacy modlar ve oyun içi sunucu overlay'i ekler. Tamamen **client-side** — diğer oyuncular hiçbir şeyi görmez.

## ✨ Özellikler

| Kategori | Açıklama |
|----------|----------|
| **Bootstrapper** | `Roblox/Versions` içinden en güncel `RobloxPlayerBeta.exe`'yi bulur, `ClientAppSettings.json` ve modları uygulayıp başlatır |
| **FastFlag Editor** | `ClientSettings/ClientAppSettings.json` okuma/yazma, tüm sürüm klasörlerine otomatik yayma |
| **Mod Manager** | `%LocalAppData%\Gravistrap\Mods` → sürüm klasörüne senkron (`content`, `PlatformContent`, `.dll`) |
| **Otomatik Güncelleme** | `clientsettingscdn` kontrol + `RobloxPlayerLauncher --app` sessiz tetikleme (tarayıcı açmaz, çoklu istemcide atlanır) |
| **Çoklu İstemci** | `ROBLOX_singletonMutex` + `ROBLOX_singletonEvent` handle'larını brute-force kapatarak 2+ client aynı anda |
| **Eski Roblox Düzeni** | Cursor / ses (`oof`) / avatar kataloğu için `%LocalAppData%\Gravistrap\Legacy` |
| **ReShade** | `d3d11.dll`, `dxgi.dll`, `ReShade.ini` sadece `UseReShade` açıksa kopyalanır |
| **Studio Eklentisi** | `%LocalAppData%\Roblox\Plugins\GravistrapPlugin.lua` otomatik kurulum |
| **Sunucu Overlay** | Oyuna girince **sunucu IP:port + lokasyon + ping (ICMP→TCP fallback) + FPS** gösterir, çıkınca kapanır, sürüklenebilir (480px) |
| **Kısayol** | Masaüstüne `Roblox'u Başlat.lnk` (`Gravistrap.exe --launch`) — aynı ayarlarla direkt başlatır |

## 📥 Kurulum

1. **Releases**'ten `Gravistrap_v2.0_TransparentLogo.zip` indir
2. Zip'i çıkar, `Gravistrap.exe` çift tıkla
   - `standalone` 72 MB, .NET gerektirmez
   - `framework-dependent` 150 KB, .NET 8 ister
3. İlk açılışta `Roblox'u Başlat` kısayolu otomatik oluşur

> Roblox en az bir kez resmi launcher ile açılmış olmalı (`%LocalAppData%\Roblox\Versions`)

## 🚀 Kullanım

- **▶ Roblox Başlat** veya masaüstündeki **Roblox'u Başlat** kısayolu
- **🎨 Görünüm** — Overlay aç/kapat + önizle
- **🚩 FastFlags** — `FIntTaskSchedulerTargetFps=144` gibi ekle/sil
- **📦 Modlar** — Mod klasörünü aç
- **🕹 Eski Roblox** — `Legacy\Cursors` ve `Legacy\Sounds` içine dosya at
- **⚙️ Davranış** — Otomatik güncelle / çoklu istemci

## 🛠 Kaynak Koddan Derleme

```powershell
winget install Microsoft.DotNet.SDK.8
git clone https://github.com/KULLANICI/Gravistrap.git
cd Gravistrap
dotnet build Gravistrap.sln -c Release
dotnet publish src/Gravistrap/Gravistrap.csproj -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -o dist/standalone
