<div align="center">

[English](../../README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)
· [Ελληνικά](README_el.md) · [മലയാളം](README_ml.md) · **Roman Urdu** · [Română](README_ro.md)
· [Ελληνικά](README_el.md) · [മലയാളം](README_ml.md) · [اردو](README_ur.md)

 <div align="center">

# REA: Reverse Engineer Anything

### بائنریز، ایپلی کیشنز اور رن ٹائم رویّے کی ریورس انجینئرنگ کے لیے ایک MCP۔

**کوئی فیچر پسند آیا؟ معلوم کریں کہ وہ کیسے کام کرتا ہے، یہاں تک کہ بائنری کی سطح تک۔**

**[Website](https://rea.tools/) · [Guides](https://rea.tools/guides/) · [Showcases](https://rea.tools/showcase/)**

[فوری آغاز](#jaldi-shuru-karein) · [REA کیسے کام کرتا ہے](#rea-kaise-kaam-karta-hai) · [کیا کچھ تجزیہ کر سکتے ہیں](#kya-kuch-analyze-kar-sakte-hain) · [عملی مثالیں](#amli-misaalein) · [RL ماحول بنائیں](#build-rl-environments) · [عمومی سوالات](#faq) · [دستاویزات](#documentation)

`npx rea-agents setup`

</div>

> [!IMPORTANT]
> REA صرف [morluto/rea](https://github.com/morluto/rea)، [rea.tools](https://rea.tools/) یا [rea-agents npm package](https://www.npmjs.com/package/rea-agents) سے حاصل کریں۔
> انسٹالیشن اور ریلیز کے لنکس انہی سرکاری ذرائع سے کھولیں۔ صرف ملتا جلتا ریپوزٹری نام یا نقل کیا ہوا README کسی ڈاؤن لوڈ کو سرکاری ثابت نہیں کرتا۔

---

کسی ایپ میں ایسا فیچر دیکھا جو آپ اپنے پروڈکٹ میں چاہتے ہیں؟ اپنے ایجنٹ سے کہیں کہ REA کے ذریعے اس کی جانچ کرے۔ وہ ایپ کا سورس کوڈ دستیاب نہ ہونے کے باوجود اسے جانچ سکتا ہے، سمجھا سکتا ہے کہ فیچر کیسے کام کرتا ہے، شواہد دکھا سکتا ہے اور آپ کے پروجیکٹ کے لیے اس کا ایک ورژن بنا سکتا ہے۔

REA آپ کے ایجنٹ کو ایسے ٹولز فراہم کرتا ہے جو Native Binaries، JavaScript اور Electron ایپس، .NET Assemblies اور ویب سائٹس کا تجزیہ کرتے ہیں۔ یہی ٹولز ٹرمینل سے بھی استعمال کیے جا سکتے ہیں۔ تجزیہ مقامی کمپیوٹر پر ہوتا ہے، اور ہر نتیجے کے ساتھ اس کے شواہد اور حدود بھی فراہم کی جاتی ہیں۔

Setup، REA کو آپ کے ایجنٹ کے ساتھ رجسٹر کرتا ہے اور اس کے مطابق ورک فلو کی ہدایات انسٹال کرتا ہے۔ Native Analysis کے لیے پہلے سے انسٹال شدہ Hopper، Ghidra یا IDA استعمال ہو سکتا ہے؛ آپ کی منظوری سے Setup، Hopper بھی انسٹال کر سکتا ہے۔ Static JavaScript Analysis کے لیے Native Analysis Engine کی ضرورت نہیں ہوتی۔

> تصویری رہنمائی، Setup کی ہدایات اور حقیقی کیس اسٹڈیز کے لیے **[REA کی ویب سائٹ دیکھیں](https://rea.tools/)**۔

## فوری آغاز

Linux پر Ghidra، JADX، Firmware Tools شروع کرنے اور Static JavaScript/Electron Analysis کے لیے REA کے `PATH` میں `ps` کا ایسا ورژن ہونا ضروری ہے جو `procps` کے ساتھ مطابقت رکھتا ہو، تاکہ پروسیس کی ملکیت کی جانچ کی جا سکے۔ مسئلہ حل کرنے کے مراحل کے لیے `docs/installation.md` میں "Linux owned-process prerequisite" کا حصہ دیکھیں۔

### اپنا ایجنٹ سیٹ اپ کریں

Node.js اور npm انسٹال ہونے کے بعد یہ کمانڈ چلائیں:

```bash
npx rea-agents setup
```

اپنے ایجنٹس منتخب کریں، مجوزہ تبدیلیاں دیکھیں اور ان کی منظوری دیں۔ Setup، REA کا MCP Server اور اس کے مطابق ورک فلو کی ہدایات شامل کرتا ہے، اور موجودہ کنفیگریشن کا بیک اپ بناتا ہے۔ اس کے بعد اپنا ایجنٹ دوبارہ شروع کریں۔

Setup، Claude Code، Codex، Cursor، Gemini CLI، Grok Build اور [دیگر ایجنٹس](../installation.md#supported-agents) کو سپورٹ کرتا ہے۔ Provider Configuration اور دستی MCP Registration کے لیے [انسٹالیشن اور سیٹ اپ](../installation.md) دیکھیں۔

Context Overhead کم رکھنے کے لیے MCP، بطورِ ڈیفالٹ مختصر Input Schemas استعمال کرتا ہے۔ اگر تمام ظاہر کردہ Fields کی رہنمائی اور Nested Validation کی تفصیلات درکار ہوں تو اپنی MCP Registration میں `REA_MCP_INPUT_SCHEMA_PROFILE=full` سیٹ کریں۔ دونوں Profiles میں تمام Tools اور Canonical Server Validation موجود رہتے ہیں۔ MCP Contracts Guide میں "Compact input schema profile" کا حصہ دیکھیں۔

### اپنے ایجنٹ سے کہیں

```text
Notes ایپ میں تلاش کا فیچر کیسے کام کرتا ہے، اس کی جانچ کرو، مجھے شواہد دکھاؤ اور میرے پروجیکٹ کے لیے اسی طرح کا فیچر بناؤ۔
```

`Notes` کی جگہ اپنی مطلوبہ ایپ اور اس فیچر کا نام لکھیں جسے آپ سمجھنا چاہتے ہیں۔

### ٹرمینل سے استعمال کریں

Extract کی گئی JavaScript/Electron ایپ کی ڈائریکٹری یا ASAR فائل کا تجزیہ کریں:

```bash
npx -y rea-agents@latest analyze-javascript-application /absolute/path/to/app --json
```

نتائج میں Modules، Imports، Electron Boundaries اور ان سے متعلق شواہد شامل ہوتے ہیں۔

Path کو اپنی مطلوبہ ایپ کے Path سے تبدیل کریں، مثلاً Windows پر `"D:/apps/example"`۔

روزمرہ استعمال کے لیے `rea` کمانڈ انسٹال کرنے کی خاطر:

```bash
npm install --global rea-agents
rea --help
```

Native Analysis سے پہلے Provider Configure کریں۔ Native Commands، Provider Selection، Snapshots اور Scripting کے لیے [CLI اور Evidence Guide](../cli.md) دیکھیں۔

### REA کو اپ ڈیٹ کریں

REA میں تیزی سے تبدیلیاں آتی ہیں اور نئی Releases میں اکثر Bug Fixes شامل ہوتی ہیں۔ اپنی انسٹالیشن کو تازہ ترین رکھیں۔

اگر CLI کو `npm install --global` یا `bun add --global` کے ذریعے انسٹال کیا ہے تو:

```bash
rea update
```

`rea --update` اسی تصدیق شدہ طریقۂ کار کا Alias ہے اور وہی Global Output Flags قبول کرتا ہے۔ دیگر کمانڈز کے ساتھ استعمال کرتے وقت `rea update` لکھیں۔

Updater Commands، `stdout` اور `stderr` کو ملا کر زیادہ سے زیادہ 4 MiB ڈیٹا محفوظ کرتی ہیں۔ کمانڈ مکمل ہونے کے بعد اس حد سے بڑے Metadata Replies مسترد کر دیے جاتے ہیں؛ Verbose Installs محدود Diagnostics کے ساتھ جاری رہتی ہیں۔ انسانی مطالعے کے لیے Progress Output، Terminal Backpressure کا خیال رکھتا ہے اور بھیجی گئی Writes مکمل ہونے کا انتظار کرتا ہے۔

Bun کی Global Updates کے لیے Bun 1.2.17 یا اس سے نیا ورژن درکار ہے۔ اگر Bun کا پرانا ورژن موجود ہو تو `rea update` چلانے سے پہلے Bun کو دستی طور پر Upgrade کریں۔

Agent Registrations اور Skills کو Refresh کرنے کے لیے Update کے Output میں دی گئی Setup Command چلائیں۔

اگر آپ `npx` استعمال کرتے ہیں تو Agent Setup اپ ڈیٹ کرنے کے لیے:

```bash
npx rea-agents@latest setup
```

Setup کی تبدیلیوں کا جائزہ لیں، انہیں منظور کریں اور ایجنٹ دوبارہ شروع کریں۔ ایک مرتبہ چلائی جانے والی CLI Commands کے لیے `npx rea-agents@latest` کے بعد مطلوبہ کمانڈ لکھیں۔ Bun کے ساتھ `npx rea-agents@latest` کی جگہ `bunx rea-agents@latest` استعمال کریں۔

## REA کیسے کام کرتا ہے

آپ کا ایجنٹ MCP کے ذریعے REA کو کال کرتا ہے تاکہ مطلوبہ ایپ یا فائل کا معائنہ کرے اور متعلقہ کوڈ کا سراغ لگائے۔ REA اپنے نتائج شواہد کے ساتھ واپس فراہم کرتا ہے۔ ایجنٹ ان نتائج کی بنیاد پر مزید سوالات کرتا ہے، رویّے کی وضاحت کرتا ہے یا اس کی بنیاد پر Implementation لکھ کر اسے ٹیسٹ کرتا ہے۔ CLI Commands بھی یہی Workflows استعمال کرتی ہیں۔

[REA کے تجزیاتی عمل کی مکمل شکل دیکھیں](../../website/public/assets/figures/rea-investigation-flow.svg)۔

## کیا کچھ تجزیہ کر سکتے ہیں

REA کے لیے Node.js 22.x (`>=22.23.4`)، 24.x (`>=24.22.1`) یا 26.12.1+ اور npm درکار ہیں۔ اضافی Tools اور Host Support کا انحصار مطلوبہ Target پر ہوتا ہے۔

| Target | REA کیا فراہم کرتا ہے | ضروریات اور رہنمائی |
|---|---|---|
| Desktop Installations | Runtime Candidates، معاون فائلیں، Component Markers اور اگلے تجزیاتی مراحل | Built-in Directory/Header Inspection؛ [Desktop Applications](../desktop-applications.md) |
| Native Binaries | Pseudocode، Assembly، Strings، Symbols، Calls اور References | Hopper، Ghidra یا IDA؛ [Native Analysis](../native-investigation.md) |
| Offline ELF Layout | Sections، Segments، Original Symbols/Relocations اور Static Mitigation Candidates | Linux x64 پر فراہم کردہ pwntools؛ [Binary Diagnostics](../binary-diagnostics.md) |
| Go Binaries | Embedded Compiler Version، Modules، Replacements اور Build Settings | Built-in Static ELF/PE/thin Mach-O Inspection؛ Go انسٹال کرنا ضروری نہیں |
| GPU Code Objects | CUDA/HIP Targets، منتخب Kernel Parameters، Resources اور محفوظ شدہ PTX Text | Built-in Static ELF/PE/fatbin/CUBIN/PTX Inspection؛ [GPU Code Objects](../gpu-code-objects.md) |
| Model Artifacts | GGUF/Safetensors Metadata، Tensor Declarations اور ان سے اخذ کردہ مجموعی اعداد | Built-in Header Inspection؛ اختیاری Full-file Hash؛ [Model Files](../model-artifacts.md) |
| IL2CPP Metadata | Unity global-metadata.dat سے Assembly Images، Type اور Method Names اور Index Ranges | Versions 24، 27، 29، 31 اور 39 کی Built-in Static Decoding؛ Unity ضروری نہیں |
| Godot PCK | Archive Inventory، Extraction، Original Header/Directory Facts اور منتخب Content Identities | Built-in Static Formats 2، 3 اور 4؛ Godot ضروری نہیں |
| Rust Binaries | Embedded cargo-auditable Crate Names، Versions، Sources اور Dependency Edges | Built-in Static ELF/PE/thin Mach-O Inspection؛ [Rust Binaries](../rust-binaries.md) |
| PE Certificates | Authenticode WIN_CERTIFICATE Entries اور PKCS#7 Signer/X.509 Identity Fields | Built-in Static PE Inspection؛ [PE Certificates](../pe-certificates.md) |
| PE Imports | Import اور Delay-load DLL Names، Ordinals، IAT RVAs اور pefile Import Hash | Built-in Static PE Inspection؛ [PE Imports](../pe-imports.md) |
| ELF Notes | PT_NOTE/SHT_NOTE Owners، Types، GNU Build-ID اور ABI-tag Fields | Built-in Static ELF Inspection؛ [ELF Notes](../elf-notes.md) |
| Linux Kernel Modules | .modinfo Keys، __versions CRCs، this_module کی موجودگی اور Signature Trailer | Built-in Static ELF Inspection؛ [Kernel Modules](../kernel-modules.md) |
| Erlang BEAM | IFF Chunks، Atoms، Exports، Imports، Lambdas اور Code Header | Built-in Static BEAM Inspection؛ [Erlang BEAM](../erlang-beam.md) |
| WASM Artifact | Validation، Sections، Exact Import/Export WAT Forms اور Decoded WAT | فراہم کردہ WABT 1.0.42؛ `inspect_wasm_artifact` |
| EVM Bytecode | Dispatch Selectors، Byte Offsets، اخذ کردہ Arguments اور Mutability | Linux x64 پر مقامی Raw/Hex Carrier؛ [Offline EVM Guide](../evm-bytecode.md) |
| SQLite Databases | Tables، Columns، Indexes، Views، Triggers اور منتخب عام Table Rows | Local Database/WAL Snapshot؛ Native SQLite Limits کے ساتھ Node.js 24.x >=24.15 یا 26+ |
| Apple IPS Crash Reports | Apple .ips Metadata، Threads، Images اور Crash Classification | Built-in Static JSON Inspection؛ [Apple IPS](../apple-ips.md) |
| JavaScript / Electron | Modules، Imports، Source Maps، Routes، IPC اور Native Add-on Relationships | Node.js اور npm؛ Linux پر procps-compatible `ps`؛ [Application Analysis](../javascript-application-workflows.md) |
| Websites | Page Structure، Scripts، Network Observations اور مطلوبہ Screenshots | Chrome-family Browser؛ [Browser Analysis](../browser-observation.md) |
| .NET Assemblies | Metadata، CIL Instructions، Declared Native Dependencies اور Build Comparisons | کسی اضافی Tool کی ضرورت نہیں؛ صرف Static Analysis؛ [Managed-code Guide](../managed-code-analysis.md) |
| Android APKs | Manifest Declarations، Classes، Decompiled Methods اور References | Linux/macOS/Windows x64 پر Headless JADX اور Full JDK؛ [Android Guide](../android-analysis.md) |
| Android Devices | Devices، Packages، Processes، Logs، Dumps، Screen Captures اور APK/File Transfers | فراہم کردہ adb؛ Emulator یا حقیقی Device؛ [ADB Guide](../adb-device-analysis.md) |
| Firmware | Regions، Extraction Results اور Native-analysis Handoffs | Linux پر Binwalk/Unblob؛ [Firmware Guide](../firmware-guide.md) |

Static JavaScript اور .NET Inspection میں ایپلی کیشن چلائے بغیر فراہم کردہ فائلیں پڑھی جاتی ہیں۔ Runtime Capture، آپ کی اجازت کے مطابق منتخب Target کو چلاتا ہے یا اس کے ساتھ تعامل کرتا ہے۔ ہر Runtime Guide میں اس کے اثرات بیان کیے جاتے ہیں۔

Offline Native Binary Inspection کے لیے REA، آپ کے فراہم کردہ GNU objdump اور Rizin کو بھی سپورٹ کرتا ہے۔ Provider Setup، CLI Commands اور Evidence کی حدود کے لیے [Reverse-engineering Tools Guide](../reverse-engineering-tools.md) دیکھیں۔ REA ان دونوں Providers کو انسٹال یا اپ ڈیٹ نہیں کرتا۔

## عملی مثالیں

### DX-Ball: Sound-pan Calculation دوبارہ بنائیں

Sound Call سے اس کے Position-to-pan Helper تک پہنچیں، Instructions کا معائنہ کریں اور نامکمل Pseudocode کو C میں تبدیل کریں۔ دوبارہ تیار کردہ Code، اصل x86 کے 3,205 Cases پاس کرتا ہے اور Compiled Function کے تمام 63 Bytes دوبارہ حاصل کرتا ہے۔

[کیس اسٹڈی پڑھیں](https://rea.tools/showcase/dx-ball/) · [Reconstruction Repository](https://github.com/N0zoM1z0/dx-ball)

### Notion: Electron Clipboard Bridge کا سراغ لگائیں

Renderer کی Clipboard API تلاش کریں، Preload اور IPC کے راستے Main Process تک اس کے بہاؤ کا سراغ لگائیں اور Rich Clipboard Format کا معائنہ کریں۔

[کیس اسٹڈی پڑھیں](https://rea.tools/showcase/notion/)

### TH04: DOS Bullet-ring Calculation حاصل کریں

اصل PC-98 گیم کی 16-bit Instructions کا معائنہ کریں، Fixed اور Aimed Angle Calculations حاصل کریں اور دوبارہ تیار کردہ C++ کو پرانے Compiler کے Output سے موازنہ کریں۔

[کیس اسٹڈی پڑھیں](https://rea.tools/showcase/th04/) · [Reconstruction Repository](https://github.com/N0zoM1z0/th04)

## RL Environments بنائیں

AI Agent کے لیے مقامی Environment بنائیں جہاں وہ اصل ایپ چلائے بغیر مسائل تلاش کرنے یا فولڈر بنانے جیسے کاموں کی مشق کر سکے۔ اسے Reinforcement Learning (RL) یا Agent کی کام مکمل کرنے کی صلاحیت جانچنے کے لیے استعمال کریں۔

REA ریکارڈ شدہ API Requests اور Responses کو ایسے Tools میں تبدیل کرتا ہے جنہیں Agent کال کر سکتا ہے۔ Environment، ریکارڈ شدہ ڈیٹا استعمال کرتا ہے اور صرف ان تبدیلیوں کی اجازت دیتا ہے جن کے اثرات Recording سے ثابت ہوتے ہیں۔

اپنی Test Web App کے مطابق مثال میں موجود URL اور فولڈر کے کام تبدیل کریں:

```text
REA کے ذریعے میری Test Web App سے ایک RL Environment بناؤ:
http://127.0.0.1:3000

فولڈرز کی فہرست، تخلیق، نام کی تبدیلی اور حذف کرنے کے کام شامل کرو۔
Test Folders بنا اور حذف کر سکتے ہو، لیکن موجودہ ڈیٹا تبدیل نہ کرو۔

اسے my-env نام کے فولڈر میں محفوظ کرو، کام کرنے والے Operations چیک کرو اور اسے چلانے کا طریقہ بتاؤ۔
```

### کمانڈ لائن استعمال کریں

یہ Commands اس وقت استعمال کریں جب ایپ کی Browser Requests اور Responses کی Recording پہلے سے فائل میں موجود ہو۔ نتیجہ چلانے کے لیے AgentEnv اور Docker بھی درکار ہیں۔

```sh
rea environment-build ./session.har ./my-env --name my-env --json
agent-env run ./my-env
```

REA ایک تیار Environment اور بنیادی Test Export کرتا ہے، جو یہ جانچتا ہے کہ Environment شروع ہوتا ہے اور جواب دیتا ہے۔ اپنے RL Framework کے مطابق Task Goals اور Reward Checks طے کریں اور Training چلائیں۔

[Environment بنانے کی رہنمائی](https://rea.tools/guides/rl-environments/) · [Environment Reference](../agent-environments.md)

## عمومی سوالات

### کون سے Agents، REA استعمال کر سکتے ہیں؟

ہر وہ Agent جو مقامی MCP Servers کو سپورٹ کرتا ہو۔ Setup، [Supported Agents](../installation.md#supported-agents) کو Configure کرتا ہے؛ دوسرے Clients، [Manual MCP Registration](../installation.md#mcp-registry) استعمال کر سکتے ہیں۔

### کیا مجھے Hopper، Ghidra یا IDA درکار ہیں؟

گہری Native Analysis کے لیے ان میں سے کسی ایک Tool کی ضرورت ہوتی ہے۔ Static JavaScript اور .NET Inspection، Native Analysis Engine کے بغیر کام کرتی ہے۔ منظوری کے بعد Setup، Hopper انسٹال کر سکتا ہے؛ Ghidra اور IDA کے لیے آپ کی موجودہ Installations استعمال ہوتی ہیں۔ [Provider Setup](../installation.md#hopper) دیکھیں۔

### کیا Hopper کو پہلے شروع کرنا ہوگا؟

جب کسی Operation کے لیے Hopper درکار ہو تو REA اسے شروع کرتا ہے۔ macOS پر پہلی مرتبہ کھلنے والا Dialog، Demo Mode منتخب کرنے یا License Activate کرنے کا کہہ سکتا ہے۔ پہلی CLI/MCP Operation یا Unattended Job سے پہلے اسی User Session میں یہ مرحلہ مکمل کریں۔ ضرورت ہو تو Hopper دستی طور پر کھولیں۔

### کیا REA میری ایپ اپ لوڈ کرتا ہے؟

REA، Targets کا تجزیہ مقامی کمپیوٹر پر کرتا ہے۔ آپ کے Agent کو Tool Results موصول ہوتے ہیں، جبکہ اس کے Model Provider کی اپنی Data Policy لاگو ہوتی ہے۔

### مسئلہ ملنے پر کیا کریں؟

پہلے REA اپ ڈیٹ کریں۔ اگر CLI کو Global طریقے سے انسٹال کیا ہے تو:

```bash
rea update
```

اگر `npx` کے ذریعے Agent Setup اپ ڈیٹ کرنا ہے تو:

```bash
npx rea-agents@latest setup
```

Setup Refresh مکمل کریں اور Agent دوبارہ شروع کریں۔ پھر وہی Task دوبارہ آزمائیں۔ مسئلہ برقرار رہنے پر REA Version، Target Type، مسئلہ دہرانے کے مراحل اور Error Output کے ساتھ [Issue کھولیں](https://github.com/morluto/rea/issues)۔

## دستاویزات

ویب سائٹ کی [عملی رہنمائی](https://rea.tools/guides/) سے آغاز کریں۔ مکمل Options، ضروریات اور Results Contracts کے لیے:

- [Installation and Setup](../installation.md): Agent Registration، Provider Configuration، Updates اور Uninstall۔
- [Readiness and Troubleshooting](../installation.md#check-readiness-for-your-task): Agent یا Analysis Engine کے مسائل کی تشخیص۔
- [CLI and Evidence](../cli.md): Commands، Provider Selection، Snapshots، Import/Export اور Exit Statuses۔
- [MCP Contracts](../mcp-contracts.md) اور [Agent Prompts](../mcp-prompts.md): Tool Results، Sessions اور Guided Investigations۔
- [Tool Catalog](../mcp-contracts.md#generated-catalog): Tools، Providers اور CLI Commands کی فہرست۔
- [Roadmap](../roadmap.md): منصوبہ بند کام اور Capability Trackers۔

سیکیورٹی کی کمزوریوں کی اطلاع [SECURITY.md](../../SECURITY.md) کے ذریعے دیں۔

## ذمہ دارانہ استعمال

ذمہ دارانہ استعمال سے متعلق ہدایات کے لیے [DISCLAIMER.md](../../DISCLAIMER.md) دیکھیں۔

غیر قانونی یا غیر مجاز استعمال کے بارے میں پروجیکٹ کا مؤقف REA کے تمام Versions، Distribution Channels اور Platforms پر لاگو ہوتا ہے۔ ہر Copy پر اس کے متعلقہ Licenses برقرار رہتے ہیں۔

REA قانونی تحقیق، تعلیم، Interoperability، Software Preservation اور ایسے Software کے تجزیے کے لیے بنایا گیا ہے جو آپ کی ملکیت ہو یا جس کی جانچ کرنے کی آپ کو اجازت حاصل ہو۔

## حصہ ڈالیں

REA میں آپ کی مدد کا خیرمقدم ہے! Bug Report کرنے یا Feature تجویز کرنے کے لیے [Issue کھولیں](https://github.com/morluto/rea/issues)، یا Code اور Documentation بہتر بنانے کے لیے [Pull Request بھیجیں](https://github.com/morluto/rea/pulls)۔

Development Setup اور Checks کے لیے [CONTRIBUTING.md](../../CONTRIBUTING.md)، Verification Lanes کے لیے [Testing](../testing.md) اور Project Structure کے لیے [Architecture Map](../architecture.mermaid) دیکھیں۔

## License

[MIT](../../LICENSE)

REA کا اپنا لکھا ہوا Code، MIT License کے تحت ہے۔ Third-party مواد کے اپنے Licenses اور Copyright Notices برقرار رہتے ہیں۔ Dependencies کی فہرست، محفوظ شدہ License Texts اور External Tools کی شرائط کے لیے [Third-party Notices](../../THIRD_PARTY_NOTICES.md) دیکھیں۔

IDA Pro / Hex-Rays Decompilers، Hopper اور JEB سمیت **تجارتی Tools کو قانونی طور پر حاصل کرنا اور ان کے متعلقہ Licenses کے مطابق استعمال کرنا ضروری ہے۔** REA کسی Tool کا License، Key یا Activation کا حق فراہم نہیں کرتا۔ Trials اور Demos پر Vendor کی شرائط لاگو ہوتی ہیں، جن میں User، Features، Automation اور Output Sharing کی پابندیاں بھی شامل ہو سکتی ہیں۔ Cracked Copies، چوری شدہ Keys، غیر مجاز Key Sharing اور License Restrictions کو نظرانداز کرنے کی اجازت نہیں۔ یہ رہنمائی MIT یا Third-party Licenses میں تبدیلی نہیں کرتی۔

