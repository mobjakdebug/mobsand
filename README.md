# mob-sand (special thanks to @maanimis)

<div dir="rtl">

# 📥 دانلود حرفه‌ای فایل با تقسیم‌بندی 7z

یک گردش‌کار گیت‌هاب که فایل‌ها را از هر لینک مستقیم دانلود کرده، در صورت نیاز به تکه‌های 95 مگابایتی تقسیم می‌کند، و با دسته‌های 5 تایی در مخزن ذخیره می‌کند — ایده‌آل برای کاربران ایرانی بدون دسترسی به هاست‌های خارجی.

---

## ⚙️ راه‌اندازی

0. این مخزن را فورک کنید
1. به تنظیمات مخزن بروید: **Settings** → **Actions** → **General**
2. در بخش **Workflow permissions** گزینه‌ی **Read and write permissions** را فعال کنید
3. ذخیره کنید.

بدون نیاز به توکن یا رمز.

---

## 🚀 نحوه‌ی استفاده

1. هر فایلی را روی گیت‌هاب ویرایش کنید (مثلاً همین `README.md` – آیکون ✏️)
2. یک تغییر کوچک بدهید (فاصله، خط خالی، …)
3. در کادر **Commit changes** پیام کامیت را به یکی از شکل‌های زیر بنویسید
4. گزینه‌ی **Commit directly to the `main` branch** را انتخاب کنید
5. روی **Commit changes** کلیک کنید

گردش‌کار اجرا شده و فایل‌ها در مسیر مشخص‌شده (یا به‌صورت خودکار در `downloads/`) ظاهر می‌شوند.

---

## 📝 دستورات

### ۱. دانلود تکی (حفظ نام اصلی)

```
download: [پرچم‌ها] [مسیر] لینک
```

پرچم‌های اختیاری:
- `--name اسم.فرمت` → نام دلخواه برای فایل خروجی
- `--split 150m` → حجم هر تکه (پیش‌فرض 95)

در صورت عدم تعیین مسیر، فایل‌ها به‌طور خودکار در `downloads/<دسته>/<نام فایل>/` دسته‌بندی می‌شوند (دسته‌ها: video, audio, image, document, other).

**مثال‌ها:**

```
download: https://example.com/video.mp4
```
→ در `downloads/video/video.mp4/` ذخیره می‌شود.

```
download: --name my_model.gguf https://huggingface.co/.../model.gguf?download=true
```
→ فایل با نام `my_model.gguf` ذخیره می‌شود.

```
download: --split 200m models/llm https://example.com/big_file.bin
```
→ فایل در پوشه‌ی `models/llm/` با تکه‌های 200 مگابایتی ذخیره می‌شود.

---

### ۲. دانلود و بسته‌بندی در ZIP

```
download-zip: [پرچم‌ها] [مسیر] لینک1 لینک2 ...
```

همه‌ی فایل‌ها را یکجا دانلود کرده، ابتدا در یک فایل ZIP قرار می‌دهد، سپس در صورت بزرگ بودن تقسیم می‌کند.

**مثال:**

```
download-zip: --name my_data.zip dataset https://example.com/part1.bin https://example.com/part2.bin
```
→ فایل‌ها در `dataset/` ذخیره و با نام `my_data.zip` (و تکه‌های `my_data.zip.7z.001` ...) قرار می‌گیرند.

---

## 📁 خروجی

- فایل‌های بزرگ‌تر از ۹۰ مگابایت به طور خودکار با 7z به تکه‌های ۹۵ مگابایتی تقسیم می‌شوند (قابل تغییر با `--split`).
- تکه‌ها با پسوند `.7z.001`، `.7z.002` و … ذخیره می‌شوند.
- برای استخراج، کافیست همه‌ی تکه‌ها را کنار هم قرار داده و با 7-Zip روی اولین تکه (`001.`) کلیک راست کرده و گزینه‌ی **Extract Here** را بزنید.

---

## 👀 پیگیری نتیجه

- تب **Actions** را باز کنید، آخرین اجرا را ببینید.
- پس از اتمام، در تب **Code** فایل‌ها را در مسیر انتخابی یا پوشه‌ی `downloads/` پیدا می‌کنید.

---

## ⚠️ نکات

- لینک‌ها باید عمومی باشند.
- گردش‌کار در کامیت‌های خود از `[skip ci]` استفاده می‌کند تا حلقه‌ی بی‌نهایت ایجاد نشود.
- اگر پیام کامیت دستور معتبری نداشته باشد، هیچ اتفاقی نمی‌افتد.

</div>

---

# 📥 Professional File Downloader with 7z Splitting

A GitHub Actions workflow that downloads files from any direct URL, automatically splits large ones into 95 MB 7z chunks, and pushes them to your repo in safe batches — perfect for users behind restrictive networks or with limited access.

---

## ⚙️ Setup

0. Fork this repository
1. Go to **Settings** → **Actions** → **General**
2. Under **Workflow permissions**, choose **Read and write permissions**
3. Save.

No tokens or secrets are required.

---

## 🚀 How to use

1. Edit any file on GitHub (e.g., this `README.md` – click the ✏️ icon)
2. Make a tiny change (a space, a blank line)
3. In the **Commit changes** box, write a commit message using one of the formats below
4. Select **Commit directly to the `main` branch**
5. Click **Commit changes**

The workflow runs automatically and the downloaded files will appear in the specified folder (or auto-organized under `downloads/`).

---

## 📝 Commands

### 1. Download individually (keeps original filename)

```
download: [flags] [target_folder] URL
```

Optional flags:
- `--name filename.ext` → custom output name
- `--split 150m` → chunk size (default: 95m)

If no target folder is given, files are automatically sorted into `downloads/<category>/<filename>/` (categories: video, audio, image, document, other).

**Examples:**

```
download: https://example.com/video.mp4
```
→ saved in `downloads/video/video.mp4/`

```
download: --name my_model.gguf https://huggingface.co/.../model.gguf?download=true
```
→ file renamed to `my_model.gguf`

```
download: --split 200m models/llm https://example.com/huge_file.bin
```
→ placed in `models/llm/` with 200 MB chunks

---

### 2. Download & pack into ZIP

```
download-zip: [flags] [target_folder] URL1 URL2 ...
```

Downloads all listed files, bundles them into a timestamped ZIP archive, then splits the archive if needed.

**Example:**

```
download-zip: --name my_data.zip dataset https://example.com/part1.bin https://example.com/part2.bin
```
→ files end up in `dataset/` as `my_data.zip.7z.001`, `.002`, …

---

## 📁 Output

- Files larger than 90 MB are automatically split into 7z chunks (default 95 MB each, adjustable with `--split`).
- Parts are named like `filename.7z.001`, `filename.7z.002`, …
- To reassemble: place all parts together, right-click the `.001` file and choose **7-Zip → Extract Here**.

---

## 👀 Checking the result

- Click the **Actions** tab to watch the workflow run.
- Once done, go back to the **Code** tab and navigate to your chosen folder or the `downloads/` directory.

---

## ⚠️ Notes

- URLs must be publicly accessible.
- The workflow uses `[skip ci]` in its own commits to avoid infinite loops.
- If no valid `download:` or `download-zip:` command is found, the workflow exits without doing anything.
