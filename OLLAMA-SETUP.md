# دليل ربط MedCare مع Ollama

## المتطلبات

1. **تثبيت Ollama** من https://ollama.com
2. **تثبيت نموذج** (اختر واحداً):

```bash
# الأفضل للعربية:
ollama pull llama3.2
# أو
ollama pull qwen2.5

# أخرى:
ollama pull mistral
ollama pull phi3
```

## التشغيل

Ollama يعمل تلقائياً في الخلفية بعد التثبيت.
للتأكد، افتح PowerShell واكتب:
```powershell
ollama list
```

## الإعدادات

عدّل ملف `.env` في مجلد المشروع:

```env
# اسم النموذج (يجب أن يكون مثبتاً)
OLLAMA_MODEL=llama3.2

# عنوان خادم Ollama
OLLAMA_URL=http://127.0.0.1:11434
```

## تشغيل الموقع

```bash
bun run dev
```

ثم افتح http://localhost:3000 واذهب لصفحة "فحص الأعراض".

## اختبار الاتصال بـ Ollama

للتأكد من عمل Ollama، افتح المتصفح على:
```
http://localhost:11434/api/tags
```
ستظهر قائمة بالنماذج المثبتة.

## استكشاف الأخطاء

### "تعذر الاتصال بـ Ollama"
- تأكد من تشغيل Ollama: شغّل `ollama serve`
- تأكد من المنفذ 11434 غير محجوز

### "النموذج غير متاح"
- حمّل النموذج: `ollama pull llama3.2`
- تحقق من الأسماء: `ollama list`

### بطء الاستجابة
- المرة الأولى تكون بطيئة (تحميل النموذج)
- استخدم نموذج أصغر مثل `phi3` أو `llama3.2` (وليس 8B)

## ربط جهاز آخر في الشبكة

إذا أردت استخدام Ollama من جهاز آخر:

1. على جهاز Ollama، شغّل:
   ```bash
   OLLAMA_HOST=0.0.0.0 ollama serve
   ```

2. على جهاز الموقع، في `.env`:
   ```env
   OLLAMA_URL=http://192.168.1.X:11434
   ```
   (استبدل X بعنوان IP الصحيح)
