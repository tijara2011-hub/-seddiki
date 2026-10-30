<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HTML → APK</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
<style>
:root{--bg:#0b0f19;--panel:#151d30;--accent:#3b82f6;--ok:#10b981;--txt:#f8fafc;--mut:#94a3b8;--bd:#23314d}
*{box-sizing:border-box;margin:0;padding:0;font-family:'Segoe UI',Tahoma,sans-serif}
body{background:var(--bg);color:var(--txt);min-height:100vh}
header{background:var(--panel);border-bottom:1px solid var(--bd);padding:1rem 1.5rem;display:flex;justify-content:space-between;align-items:center;position:sticky;top:0;z-index:5;gap:1rem}
.logo{color:var(--accent);font-weight:bold;font-size:1.2rem}
.wrap{display:grid;grid-template-columns:1fr 340px;gap:1.2rem;padding:1.2rem;max-width:1500px;margin:auto}
@media(max-width:1000px){.wrap{grid-template-columns:1fr}}
.card{background:var(--panel);border:1px solid var(--bd);border-radius:14px;padding:1.1rem;display:flex;flex-direction:column;gap:.9rem;margin-bottom:1.2rem}
.row{display:flex;gap:.5rem;flex-wrap:wrap;align-items:center;justify-content:space-between}
.btn{background:var(--accent);color:#fff;border:0;padding:.6rem 1.1rem;border-radius:8px;cursor:pointer;font-weight:600;display:inline-flex;gap:.5rem;align-items:center}
.btn.ok{background:var(--ok)}.btn.sec{background:#334155}
.btn:disabled{opacity:.5}
textarea{width:100%;height:340px;background:#060911;color:#e2e8f0;border:1px solid var(--bd);border-radius:10px;padding:.9rem;font-family:Consolas,monospace;font-size:.9rem;direction:ltr;text-align:left;resize:vertical;outline:none}
input[type=text],input[type=number],select{background:#060911;border:1px solid var(--bd);color:var(--txt);padding:.6rem;border-radius:8px;width:100%;outline:none}
label{font-size:.82rem;color:var(--mut);font-weight:600}
.g{display:flex;flex-direction:column;gap:.35rem}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:.9rem}
.chk{display:flex;gap:.5rem;align-items:center;font-size:.9rem;color:var(--txt)}
.ip{width:60px;height:60px;border-radius:12px;background:#060911;border:1px solid var(--bd);display:flex;align-items:center;justify-content:center;overflow:hidden}
.ip img{width:100%;height:100%;object-fit:cover}
.phone{width:280px;height:560px;background:#000;border:10px solid var(--bd);border-radius:36px;overflow:hidden;margin:auto}
.phone iframe{width:100%;height:100%;border:0;background:#fff}
.hide{display:none}
#log{font-size:.82rem;color:var(--mut);line-height:1.7;white-space:pre-wrap}
ol{padding-inline-start:1.2rem;font-size:.88rem;color:var(--mut);line-height:1.9}
</style>
</head>
<body>
<header>
  <div class="logo"><i class="fa-solid fa-mobile-screen-button"></i> محول HTML إلى APK</div>
  <button class="btn ok" id="buildBtn" onclick="buildProject()"><i class="fa-solid fa-hammer"></i> بناء المشروع</button>
</header>

<div class="wrap">
<div>
  <div class="card">
    <div class="row">
      <h3><i class="fa-solid fa-code"></i> الكود</h3>
      <div style="display:flex;gap:.5rem">
        <button class="btn sec" onclick="fi.click()"><i class="fa-solid fa-file-import"></i> استيراد</button>
        <input type="file" id="fi" class="hide" accept=".html,.htm,.txt" onchange="importFile(event)">
        <button class="btn" onclick="preview()"><i class="fa-solid fa-play"></i> معاينة</button>
      </div>
    </div>
    <textarea id="code" spellcheck="false"><!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{font-family:sans-serif;background:#0f172a;color:#fff;min-height:100vh;display:flex;justify-content:center;align-items:center;margin:0;text-align:center}
button{background:#10b981;border:0;padding:12px 28px;color:#fff;border-radius:50px;font-size:1rem;margin-top:16px}
</style>
</head>
<body>
<div><h1>تطبيقي الجديد 🚀</h1><p>يعمل داخل WebView على أندرويد</p>
<button onclick="alert('يعمل!')">تجربة</button></div>
</body>
</html></textarea>
  </div>

  <div class="card">
    <h3><i class="fa-solid fa-gears"></i> إعدادات التطبيق</h3>
    <div class="grid2">
      <div class="g"><label>اسم التطبيق</label><input type="text" id="name" value="تطبيقي"></div>
      <div class="g"><label>اسم الحزمة (Package ID)</label><input type="text" id="pkg" value="com.mycompany.myapp" dir="ltr"></div>
      <div class="g"><label>رقم الإصدار</label><input type="text" id="ver" value="1.0" dir="ltr"></div>
      <div class="g"><label>اتجاه الشاشة</label>
        <select id="ori"><option value="unspecified">تلقائي</option><option value="portrait">عمودي</option><option value="landscape">أفقي</option></select></div>
    </div>
    <div class="g"><label>المصدر</label>
      <select id="mode" onchange="urlBox.classList.toggle('hide',this.value!=='url')">
        <option value="local">الكود أعلاه (يُضمَّن داخل التطبيق)</option>
        <option value="url">رابط موقع (URL)</option></select></div>
    <div class="g hide" id="urlBox"><label>رابط الموقع</label><input type="text" id="url" value="https://example.com" dir="ltr"></div>
    <label class="chk"><input type="checkbox" id="full" checked> ملء الشاشة (إخفاء شريط الحالة)</label>
    <div class="g"><label>أيقونة التطبيق</label>
      <div class="row" style="justify-content:flex-start;gap:1rem">
        <div class="ip" id="ipv"><i class="fa-solid fa-image" style="color:var(--mut)"></i></div>
        <button class="btn sec" onclick="ifile.click()"><i class="fa-solid fa-image"></i> اختيار صورة</button>
        <input type="file" id="ifile" class="hide" accept="image/*" onchange="loadIcon(event)">
      </div>
    </div>
  </div>

  <div class="card">
    <h3><i class="fa-solid fa-list-check"></i> كيف تحصل على ملف APK؟</h3>
    <ol>
      <li>اضغط «بناء المشروع» لتحميل ملف ZIP.</li>
      <li>أنشئ مستودعاً جديداً على GitHub وارفع محتويات الـ ZIP كما هي (بعد فك الضغط).</li>
      <li>افتح تبويب <b>Actions</b> وانتظر دقيقتين تقريباً حتى ينتهي البناء.</li>
      <li>من نتيجة التشغيل حمّل <b>app-debug</b> وفيه ملف APK جاهز للتثبيت.</li>
    </ol>
    <p style="font-size:.8rem;color:var(--mut)">أو افتح المجلد في Android Studio واختر Build → Build APK.</p>
    <div id="log"></div>
  </div>
</div>

<div class="card" style="height:fit-content">
  <h3><i class="fa-solid fa-mobile-retro"></i> المعاينة</h3>
  <div class="phone"><iframe id="pv" sandbox="allow-scripts allow-modals"></iframe></div>
</div>
</div>

<script>
const $ = id => document.getElementById(id);
let iconImg = null;

function preview(){ $('pv').srcdoc = $('code').value; }
function importFile(e){
  const f = e.target.files[0]; if(!f) return;
  const r = new FileReader();
  r.onload = ev => { $('code').value = ev.target.result; preview(); };
  r.readAsText(f);
}
function loadIcon(e){
  const f = e.target.files[0]; if(!f) return;
  const r = new FileReader();
  r.onload = ev => {
    const img = new Image();
    img.onload = () => { iconImg = img; $('ipv').innerHTML = ''; const c = document.createElement('img'); c.src = ev.target.result; $('ipv').appendChild(c); };
    img.src = ev.target.result;
  };
  r.readAsDataURL(f);
}
function log(m){ $('log').textContent += m + '\n'; }
function xml(s){ return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,"\\'"); }

function iconBlob(size){
  return new Promise(res => {
    const c = document.createElement('canvas'); c.width = c.height = size;
    const x = c.getContext('2d');
    if(iconImg){
      x.drawImage(iconImg, 0, 0, size, size);
    } else {
      x.fillStyle = '#3b82f6'; x.fillRect(0, 0, size, size);
      x.fillStyle = '#fff'; x.font = 'bold ' + (size * .55) + 'px sans-serif';
      x.textAlign = 'center'; x.textBaseline = 'middle';
      x.fillText(($('name').value.trim()[0] || 'A'), size / 2, size / 2 + size * .03);
    }
    c.toBlob(res, 'image/png');
  });
}

async function buildProject(){
  $('log').textContent = '';
  const name = $('name').value.trim() || 'MyApp';
  const pkg = $('pkg').value.trim();
  const ver = $('ver').value.trim() || '1.0';
  const ori = $('ori').value;
  const full = $('full').checked;
  const isUrl = $('mode').value === 'url';
  const target = isUrl ? $('url').value.trim() : 'file:///android_asset/index.html';

  if(!/^[a-z][a-z0-9_]*(\.[a-z][a-z0-9_]*)+$/.test(pkg)){ alert('اسم الحزمة غير صالح. مثال: com.mycompany.myapp (أحرف صغيرة إنجليزية فقط)'); return; }
  if(isUrl && !/^https?:\/\//.test(target)){ alert('الرابط يجب أن يبدأ بـ http:// أو https://'); return; }

  $('buildBtn').disabled = true;
  try{
    const z = new JSZip();
    const dir = 'app/src/main/java/' + pkg.replace(/\./g, '/');

    z.file('settings.gradle', "pluginManagement {\n    repositories { google(); mavenCentral(); gradlePluginPortal() }\n}\ndependencyResolutionManagement {\n    repositories { google(); mavenCentral() }\n}\nrootProject.name = \"WebApp\"\ninclude ':app'\n");
    z.file('build.gradle', "plugins {\n    id 'com.android.application' version '8.5.0' apply false\n}\n");
    z.file('gradle.properties', "org.gradle.jvmargs=-Xmx2048m\nandroid.useAndroidX=false\nandroid.nonTransitiveRClass=true\n");
    z.file('app/build.gradle',
"plugins {\n    id 'com.android.application'\n}\n\nandroid {\n    namespace '" + pkg + "'\n    compileSdk 34\n\n    defaultConfig {\n        applicationId '" + pkg + "'\n        minSdk 21\n        targetSdk 34\n        versionCode 1\n        versionName '" + ver.replace(/'/g,'') + "'\n    }\n    buildTypes {\n        release { minifyEnabled false }\n    }\n    compileOptions {\n        sourceCompatibility JavaVersion.VERSION_17\n        targetCompatibility JavaVersion.VERSION_17\n    }\n}\n");

    z.file('app/src/main/AndroidManifest.xml',
'<?xml version="1.0" encoding="utf-8"?>\n<manifest xmlns:android="http://schemas.android.com/apk/res/android">\n    <uses-permission android:name="android.permission.INTERNET" />\n    <application\n        android:label="@string/app_name"\n        android:icon="@mipmap/ic_launcher"\n        android:usesCleartextTraffic="true"\n        android:theme="@android:style/Theme.DeviceDefault.NoActionBar">\n        <activity\n            android:name=".MainActivity"\n            android:exported="true"\n            android:screenOrientation="' + ori + '"\n            android:configChanges="orientation|screenSize|keyboardHidden">\n            <intent-filter>\n                <action android:name="android.intent.action.MAIN" />\n                <category android:name="android.intent.category.LAUNCHER" />\n            </intent-filter>\n        </activity>\n    </application>\n</manifest>\n');

    z.file('app/src/main/res/values/strings.xml', '<?xml version="1.0" encoding="utf-8"?>\n<resources>\n    <string name="app_name">' + xml(name) + '</string>\n</resources>\n');

    const java =
'package ' + pkg + ';\n\n' +
'import android.app.Activity;\nimport android.os.Bundle;\nimport android.view.KeyEvent;\nimport android.view.WindowManager;\nimport android.webkit.WebChromeClient;\nimport android.webkit.WebSettings;\nimport android.webkit.WebView;\nimport android.webkit.WebViewClient;\n\n' +
'public class MainActivity extends Activity {\n    private WebView web;\n\n' +
'    @Override\n    protected void onCreate(Bundle b) {\n        super.onCreate(b);\n' +
(full ? '        getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);\n' : '') +
'        web = new WebView(this);\n        WebSettings s = web.getSettings();\n        s.setJavaScriptEnabled(true);\n        s.setDomStorageEnabled(true);\n        s.setAllowFileAccess(true);\n        s.setMediaPlaybackRequiresUserGesture(false);\n        web.setWebViewClient(new WebViewClient());\n        web.setWebChromeClient(new WebChromeClient());\n' +
'        web.loadUrl(' + JSON.stringify(target) + ');\n        setContentView(web);\n    }\n\n' +
'    @Override\n    public boolean onKeyDown(int k, KeyEvent e) {\n        if (k == KeyEvent.KEYCODE_BACK && web.canGoBack()) { web.goBack(); return true; }\n        return super.onKeyDown(k, e);\n    }\n}\n';
    z.file(dir + '/MainActivity.java', java);

    if(!isUrl) z.file('app/src/main/assets/index.html', $('code').value);

    const sizes = {mdpi:48, hdpi:72, xhdpi:96, xxhdpi:144, xxxhdpi:192};
    for(const [d, s] of Object.entries(sizes)){
      z.file('app/src/main/res/mipmap-' + d + '/ic_launcher.png', await iconBlob(s));
    }

    z.file('.github/workflows/build.yml',
"name: Build APK\non:\n  push:\n    branches: [ main, master ]\n  workflow_dispatch:\njobs:\n  build:\n    runs-on: ubuntu-latest\n    steps:\n      - uses: actions/checkout@v4\n      - uses: actions/setup-java@v4\n        with:\n          distribution: temurin\n          java-version: '17'\n      - uses: gradle/actions/setup-gradle@v3\n        with:\n          gradle-version: '8.7'\n      - name: Build debug APK\n        run: gradle assembleDebug --no-daemon\n      - uses: actions/upload-artifact@v4\n        with:\n          name: app-debug\n          path: app/build/outputs/apk/debug/*.apk\n");

    z.file('README.txt', "1) ارفع كل هذه الملفات إلى مستودع GitHub جديد (الفرع main).\n2) افتح Actions وانتظر انتهاء Build APK.\n3) حمّل app-debug من نتيجة التشغيل ففيه ملف APK.\n\nأو افتح المجلد في Android Studio ثم Build > Build APK(s).\n");

    const blob = await z.generateAsync({type:'blob'});
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = pkg + '_project.zip';
    document.body.appendChild(a); a.click(); a.remove();
    log('✅ تم إنشاء المشروع. اتبع الخطوات أعلاه للحصول على APK.');
  }catch(err){
    log('❌ خطأ: ' + err.message);
  }
  $('buildBtn').disabled = false;
}

preview();
</script>
</body>
</html>
