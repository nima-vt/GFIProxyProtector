<!-- markdownlint-disable MD034 -->
# GFI Proxy Protector - محافظ سرور پروکسی ایرانی

**اطلاعیه: استفاده از این اسکریپت یا هرگونه تعلقات آن برای حامیان رژیم جنایتکار و اشغالگر جمهوری اسلامی مطلقا ممنوع و شرعا حرام است!**

## مسئله

با خرید و راه اندازی سامانه GFW توسط رژیم اشغالگر جمهوری اسلامی اکثر پروتکل های رایج  VPN در ایران مسدود شده اند و در حال حاضر تعداد معدودی پروتکل امکان اتصال دارند که از آنها در راه اندازی وبسایت ها و اپلیکشن ها بکار گرفته می‌شود به معنای دیگر مسدود کردن آنها موجب اختلال در عملکرد این  خدمات خواهد بود.

طراحان مزدور GFW برای حل این معضل ابزاری را طراحی نمودند که از آن با نام Active Probing یا کاوش فعال یاد می‌شود. این ابزار به شکل رباتی به سرورهای مشکوک مراجعه کرده و تلاش می‌کند فاکتور هایی را بیابد که در وبسایت های واقعی یافته می‌شوند و در غیر این صورت استنباط می‌کند که سرور شما یک  سرور پروکسی است و با گزارش نتیجه ی مثبت، IP سرور شما مسدود خواهد شد.

به نظر می‌رسد این سامانه از یک فهرست سفید بهره می‌برد که شامل سرویس های شناخته شده وب اعم از گوگل و کلادفلر و ... می‌ باشد و هر درخواستی به سایر وبسایت های خارج از این فهرست را مورد بررسی قرار می‌دهد! همچنین به یافته ی کاربران، بازدید از وبسایت ها و خدمات بومی کشور در هنگام متصل بودن پروکسی موجب برگشت اتصال و برملا شدن آی‌پی سرور به عنوان یک سرور پروکسی می‌شود و هرگونه شک و شبهه ی این سامانه را در پروکسی بودن سرور شما را به یقین تبدیل خواهد نمود!

## راه حل

کاربران چینی برای حل این مشکل تدبیری به نام Fallback Website در نرم‌افزار های پروکسی اندیشدند تا در صورت دریافت درخواست های بازدیدی که شاخص های نادرست یک پروکسی مثل رمز عبور یا مسیر وب غلط را داشت به پروسه ای ارجاع داده شود که مسئول نمایش فایل های ساختگی HTML می‌باشد و سرور به عنوان یک وب سرور معمولی ارائه شود. در حالیکه پیشنهاد اکید می‌کنیم شما نیز این موارد را در سرورهای پروکسی خود رعایت کنید اما می‌توانید یک قدم فراتر از این اقدامات رفته و هرگونه اتصال از جانب این شبکه های متخاصم را به سرور تان توسط این اسکریپت مسدود نمایید.

طبق مشاهدات و آزمایش ها، سامانه GFW برای این منظور از نود های مختلفی در دیتاسنتر های مختلفی اعم از Linode، AWS و DigitalOcean به عنوان بازوی عملیاتی بهره می‌برد که از یک نود مرکزی C&C در چین فرمان دریافت می‌کنند که آدرس آی‌پی مشخصی نداشته و هربار یک آی‌پی از تمام آی‌پی های چینی را برای این هدف قرض می‌گیرد. مسدودسازی این شبکه ها فرایند پیچیده تری دارد که مستلزم دانستن پیکربندی پروکسی های شماست و در حال حاضر از محدوده این اسکریپت خارج است اما در اسکریپ رنگین کمان [Rainb0w](https://github.com/redpilllabs/Rainb0w) این قابلیت فراهم شده و می‌توانید برای راه اندازی پروکسی های خود و بهره مندی از نهایت محافظت استفاده کنید.

این اسکریپت در حال حاضر دو گزینه در اختیار شما قرار می‌دهد

- مسدود کردن اتصالات *خروجی* به سمت ایران برای جلوگیری از لو رفتن سرور
- مسدود کردن تمام اتصالات ورودی و خروجی به/از سمت چین

## نحوه اجرا

```
apt install git
git clone https://github.com/redpilllabs/GFIProxyProtector.git
./run.sh
```

## نکات

- این اسکریپت «پروکسی-آگنوستیک» می‌باشد، به این معنی که تفاوتی نمی‌کند از چه اسکریپت یا پنلی برای نصب پروکسی خود اقدام نموده اید چون مستقیما روی کنترل اتصالات توسط هسته عمل می‌نماید.
- در صورت فعالسازی محافظت ورودی، هرگونه تلاش اتصال از آی‌پی های چینی در فایل لاگ هسته در مسیر `var/log/kern.log/` با پسوند GFW قابل مشاهده خواهد بود.
- این اسکریپت زیرمجموعه ای اسکریپت نصاب پروکسی رنگین کمان [Rainb0w](https://github.com/redpilllabs/Rainb0w) می‌باشد که علاوه برا این امکانات، قابلیت مسدودسازی تمام اتصالات ورودی غیر از ایران و کلادفلر، مسدود سازی تمام دامنه های [ir.] و راه اندازی یک وبلاگ وردپرس نمایشی را به عنوان Fallback decoy را نیز دارا می‌باشد.

## منابع

- [صفحه ی اصلی ماژول](https://inai.de/projects/xtables-addons/geoip.php)
