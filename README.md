AI Destekli PID Kontrol Simülasyonu

Bu proje, bulanık mantık (fuzzy logic) ile desteklenmiş bir PID (Proportional-Integral-Derivative) kontrol sisteminin Python'daki bir simülasyonunu içerir. Sistem, bir sıcaklık kontrol senaryosunu modelleyerek, zamanla değişen dinamik hedef değerleri (setpoint) takip etme yeteneğini gösterir. Kullanıcılar, farklı non-lineer hedef fonksiyonlarını kolayca seçebilir ve sistemin performansını görselleştirebilir.

Projenin Amacı

Geleneksel PID kontrolörün performansını artırmak için bulanık mantık entegrasyonunu göstermek.
Dinamik ve non-lineer hedef değerleri (örneğin, sinüs dalgası, kare dalga, üstel büyüme) takip edebilen adaptif bir kontrol sistemi oluşturmak.
Kullanıcıların hedef fonksiyonunu kolayca değiştirebilmesine olanak tanımak.
Gereksinimler
Aşağıdaki Python kütüphanelerine ihtiyaç vardır:

numpy: Matematiksel işlemler ve diziler için.
matplotlib: Grafik çizimi ve görselleştirme için.
scikit-fuzzy: Bulanık mantık uygulamaları için.
Kurulum komutları:
pip install numpy matplotlib scikit-fuzzy

Kodun Yapısı ve Çalışma Mantığı
Kod, bir sıcaklık kontrol sistemini simüle eder ve aşağıdaki temel bileşenlerden oluşur:

Sistem Modeli
Basit bir 1. dereceden diferansiyel denklemle modellenmiştir:
dT/dt = -a * T + b * u
Burada:
T: Sıcaklık (çıktı).
u: Kontrol sinyali (PID çıkışı).
a = 0.1: Sistem sabiti.
b = 0.5: Kontrol etkisi.
PID Kontrolör
Klasik PID kontrolör formülü kullanılır:
u(t) = Kp * e(t) + Ki * ∫ e(t) dt + Kd * de(t)/dt
e(t): Hata (hedef değer - gerçek değer).
Kp, Ki, Kd: Dinamik olarak bulanık mantıkla ayarlanan kazançlar.
Bulanık Mantık Entegrasyonu
Girişler:
Hata (e(t)): -50 ile 50 arasında.
Hata değişim oranı (Δe(t)): -10 ile 10 arasında.
Çıkışlar:
Kp: 0 ile 2 arasında.
Ki: 0 ile 0.5 arasında.
Kd: 0 ile 1 arasında.
Kurallar: 9 farklı bulanık mantık kuralı, hata ve hata değişim oranının tüm kombinasyonlarını kapsar. Örneğin:
Eğer hata büyük ve pozitifse, Kp yüksek, Ki düşük, Kd yüksek olur.
Dinamik Hedef Değer (Setpoint)
setpoint_function(t, function_type) fonksiyonu, zamanla değişen hedef değerleri üretir.
Kullanıcı, selected_function değişkeniyle şu fonksiyonlardan birini seçebilir:
'sine': Sinüs dalgası (50 + 20 * sin(0.1 * t)).
'square': Kare dalga (50 + 20 * sign(sin(0.1 * t))).
'exponential': Üstel büyüme (50 * (1 - e^(-0.05 * t))).
'custom': Özel kombinasyon (50 + 10 * cos(0.2 * t) + 15 * sin(0.1 * t)).
Simülasyon ve Görselleştirme
Simülasyon, 100 saniye boyunca 0.1 saniyelik zaman adımlarıyla çalışır.
Çıktılar (sıcaklık) ve hedef değerler bir grafikte görselleştirilir.
Kullanım

Kodu bir Python dosyasına (örneğin, ai_pid_control.py) kopyalayın.
Gerekli kütüphaneleri yükleyin (yukarıdaki komutla).
Hedef fonksiyonu seçmek için selected_function değişkenini değiştirin: selected_function = 'square' # Kare dalga için
Kodu çalıştırın: python ai_pid_control.py
Çıkan grafikte sistemin seçilen hedef fonksiyonunu nasıl takip ettiğini gözlemleyin.
Özelleştirme

Yeni Hedef Fonksiyon Ekleme:
setpoint_function içinde yeni bir elif dalı ekleyin: elif function_type == 'logarithmic': return 50 + 20 * np.log1p(t) Ardından selected_function = 'logarithmic' ile test edin.
Sistem Parametrelerini Değiştirme:
a, b, veya simülasyon süresini (sim_time) ihtiyaçlarınıza göre ayarlayabilirsiniz.
Örnek Çıktı

selected_function = 'sine': Hedef, 30°C ile 70°C arasında sinüsoidal bir dalga çizer.
selected_function = 'exponential': Hedef, 0°C'den 50°C'ye üstel bir şekilde yaklaşır.
Notlar

Eğer bulanık mantık hesaplama hatası alırsanız, giriş değerlerinin (error, delta_error) tanımlı aralıklarda olduğundan emin olun.
Daha karmaşık sistemler için fiziksel bir modeli entegre edebilirsiniz.
Lisans
Bu proje, MIT Lisansı altında açık kaynaktır. Detaylar için LICENSE dosyasına bakın
git add LICENSE README.md
git commit -m "Lisans ve README eklendi"
git push origin main
