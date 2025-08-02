<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fashion Post - Caption & Song Generator</title>
    <style>
        /* CSS untuk tampilan yang modern dan responsif */
        :root {
            --primary-color: #28a745; /* Warna hijau yang lebih segar */
            --secondary-color: #6c757d;
            --background-color: #f8f9fa;
            --surface-color: #ffffff;
            --text-color: #212529;
            --border-color: #dee2e6;
            --success-color: #007bff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background-color: var(--background-color);
            color: var(--text-color);
            line-height: 1.6;
            padding: 1rem;
        }

        .container {
            max-width: 800px;
            margin: 2rem auto;
            padding: 2rem;
            background-color: var(--surface-color);
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            border: 1px solid var(--border-color);
        }

        header {
            text-align: center;
            margin-bottom: 2.5rem;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 1.5rem;
        }

        h1 {
            color: var(--primary-color);
            font-size: 2rem;
            margin-bottom: 0.5rem;
        }
        
        header p {
            color: var(--secondary-color);
            font-size: 1rem;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        label {
            display: block;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--text-color);
        }

        input[type="text"],
        input[type="url"],
        textarea,
        select {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        input[type="text"]:focus,
        input[type="url"]:focus,
        textarea:focus,
        select:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(40, 167, 69, 0.2);
        }

        textarea {
            resize: vertical;
            min-height: 100px;
        }

        .input-separator {
            text-align: center;
            margin: 1rem 0;
            color: var(--secondary-color);
            font-weight: 500;
        }

        #imagePreview {
            margin-top: 1rem;
            text-align: center;
        }

        #imagePreview img {
            max-width: 100%;
            max-height: 200px;
            border-radius: 8px;
            border: 1px solid var(--border-color);
        }

        .submit-btn {
            display: block;
            width: 100%;
            padding: 0.85rem;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s, transform 0.1s;
        }

        .submit-btn:hover {
            background-color: #218838;
        }
        
        .submit-btn:active {
            transform: scale(0.99);
        }

        #results {
            margin-top: 2.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid var(--border-color);
        }

        .hidden {
            display: none;
        }

        .result-card {
            background-color: #f8f9fa;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            position: relative;
        }
        
        .result-card h3 {
            margin-bottom: 1rem;
            color: var(--primary-color);
        }

        .result-card p {
            margin-bottom: 1rem;
            white-space: pre-wrap; /* Agar baris baru di caption tetap ada */
        }
        
        .result-card .hashtags {
            color: var(--secondary-color);
            font-style: italic;
            word-wrap: break-word;
        }
        
        .result-card .song-recommendation {
            margin-top: 1.5rem;
            padding-top: 1rem;
            border-top: 1px dashed var(--border-color);
        }
        
        .song-recommendation strong {
            display: block;
            margin-bottom: 0.25rem;
        }
        
        .song-recommendation em {
             font-size: 0.9rem;
             color: var(--secondary-color);
        }

        .copy-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            padding: 0.4rem 0.8rem;
            background-color: var(--secondary-color);
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.8rem;
            transition: background-color 0.2s;
        }
        
        .copy-btn:hover {
            background-color: #5a6268;
        }

        /* Responsif untuk layar mobile */
        @media (max-width: 600px) {
            .container {
                margin: 1rem auto;
                padding: 1.5rem;
            }
            h1 {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Fashion Post Generator</h1>
            <p>Dapatkan ide caption & lagu untuk postingan baju Anda secara instan.</p>
        </header>

        <form id="generatorForm">
            <div class="form-group">
                <label for="brandName">Nama Brand / Usaha Anda</label>
                <input type="text" id="brandName" placeholder="Contoh: UrbanStyle ID" required>
            </div>
            
            <fieldset style="border:1px solid var(--border-color); padding: 1rem; border-radius: 8px; margin-bottom: 1.5rem;">
                <legend style="padding: 0 0.5rem; font-weight: 600;">Informasi Produk Baju (Pilih Salah Satu)</legend>
                
                <div class="form-group">
                    <label for="imageUpload">1. Upload Foto Baju</label>
                    <input type="file" id="imageUpload" accept="image/*">
                    <div id="imagePreview"></div>
                </div>

                <div class="input-separator">--- ATAU ---</div>

                <div class="form-group">
                    <label for="productLink">2. Paste Link Produk</label>
                    <input type="url" id="productLink" placeholder="https://tokopedia.com/link-produk-anda">
                </div>
                
                <div class="input-separator">--- ATAU ---</div>

                <div class="form-group">
                    <label for="productDescription">3. Deskripsikan Baju Anda</label>
                    <textarea id="productDescription" rows="4" placeholder="Contoh: Kemeja flanel lengan panjang, motif kotak-kotak warna biru navy dan putih."></textarea>
                </div>
            </fieldset>

            <div class="form-group">
                <label for="tone">Gaya Bahasa / Vibe yang Diinginkan</label>
                <select id="tone">
                    <option value="Kasual dan Ramah">Kasual dan Ramah</option>
                    <option value="Profesional dan Informatif">Profesional dan Informatif</option>
                    <option value="Ceria dan Enerjik">Ceria dan Enerjik</option>
                    <option value="Elegan dan Mewah">Elegan dan Mewah</option>
                    <option value="Edgy dan Berani">Edgy dan Berani</option>
                    <option value="Minimalis dan Tenang">Minimalis dan Tenang</option>
                    <option value="Emosional dan Menyentuh">Emosional dan Menyentuh</option>
                </select>
            </div>

            <button type="submit" class="submit-btn">Generate Konten!</button>
        </form>

        <div id="results" class="hidden">
            <!-- Hasil akan digenerate oleh JavaScript di sini -->
        </div>
    </div>

    <script>
    // --- DATABASE TEMPLATE ---
    const templates = {
        'Kasual dan Ramah': {
            captions: [
                "Outfit check! ✨ {product} dari {brand} ini bener-bener game changer buat daily look kamu. Nyaman, stylish, dan pastinya bikin mood auto-naik!",
                "Siap-siap jadi pusat perhatian! 😉 {product} terbaru dari {brand} ini pas banget buat nemenin nongkrong atau jalan-jalan santai. Kamu suka warna apa?",
                "Gaya santai, tapi tetap kece? Bisa banget! Cukup paduin {product} dari {brand} ini dengan jeans favoritmu. Simple, kan?",
            ],
            ctas: ["Langsung klik link di bio buat order ya!", "Cek koleksi lengkapnya di profil kami!", "Komen di bawah, kira-kira cocok dipakai ke mana nih?"],
            songs: [
                { title: "Sisa Rasa", artist: "Mahalini", reason: "Lagu pop yang easy-listening dan populer, cocok untuk audiens muda." },
                { title: "As It Was", artist: "Harry Styles", reason: "Vibe-nya yang retro dan catchy pas banget untuk gaya kasual." },
                { title: "To The Bone", artist: "Pamungkas", reason: "Lagu santai yang sudah sangat dikenal, menciptakan nuansa yang akrab." }
            ]
        },
        'Elegan dan Mewah': {
            captions: [
                "Definisi keanggunan sejati. Perkenalkan, {product} eksklusif dari {brand}, dirancang untuk setiap momen berharga Anda.",
                "Sentuhan kemewahan dalam setiap jahitan. {product} dari {brand} ini memadukan material premium dengan desain yang tak lekang oleh waktu.",
                "Tingkatkan pesona Anda dengan {product} dari koleksi terbaru {brand}. Sebuah investasi untuk penampilan yang sempurna.",
            ],
            ctas: ["Dapatkan koleksi eksklusif ini melalui link di bio.", "Hubungi kami untuk pemesanan pribadi.", "Lihat detail kemewahannya di website kami."],
            songs: [
                { title: "Sang Dewi", artist: "Lyodra, Andi Rianto", reason: "Nuansa megah dan vokal yang kuat memberikan kesan mewah." },
                { title: "Diamonds", artist: "Rihanna", reason: "Judul dan liriknya secara langsung berasosiasi dengan kemewahan." },
                { title: "Skyfall", artist: "Adele", reason: "Musik orkestra yang sinematik menciptakan atmosfer yang elegan dan premium." }
            ]
        },
        'Ceria dan Enerjik': {
            captions: [
                "Warna baru, semangat baru! 🌈 {product} dari {brand} siap bikin hari-harimu makin berwarna dan penuh energi. Let's go!",
                "Boost your energy! {product} dari {brand} ini punya desain yang fun dan siap nemenin semua aktivitas seru kamu. Siap tampil beda?",
                "Saatnya bersinar! ✨ Dengan {product} dari {brand}, tunjukkan sisi ceriamu dan sebarkan positive vibes ke sekelilingmu!",
            ],
            ctas: ["Shop now and spread the joy!", "Dapetin sekarang juga, jangan sampai kehabisan!", "Tag temanmu yang butuh suntikan semangat!"],
            songs: [
                { title: "Hype Boy", artist: "NewJeans", reason: "Beat yang adiktif dan nuansa K-Pop yang ceria sangat cocok untuk konten enerjik." },
                { title: "Selamat Pagi", artist: "RAN", reason: "Lagu lokal yang optimis dan langsung memberikan semangat pagi." },
                { title: "Good 4 U", artist: "Olivia Rodrigo", reason: "Beat pop-punk yang powerful memberikan energi yang meledak-ledak." }
            ]
        },
        'Profesional dan Informatif': {
            captions: [
                "Tampil profesional tidak pernah semudah ini. {product} dari {brand} kami dibuat dari bahan berkualitas tinggi yang menjamin kenyamanan sepanjang hari kerja Anda.",
                "Detail Produk: {product}. Produk ini menawarkan durabilitas dan desain yang smart-casual, cocok untuk lingkungan kerja modern.",
                "Investasi cerdas untuk wardrobe profesional Anda. {product} dari {brand} memberikan keseimbangan sempurna antara fungsi, kenyamanan, dan gaya formal.",
            ],
            ctas: ["Lihat spesifikasi lengkap di website kami.", "Tersedia dalam berbagai ukuran. Cek link di bio.", "Shop our workwear collection now."],
            songs: [
                { title: "Feeling Good", artist: "Michael Bublé", reason: "Lagu yang sophisticated dan memberikan rasa percaya diri." },
                { title: "Corporate", artist: "Kinematic", reason: "Musik instrumental yang modern dan tidak mengganggu, cocok untuk presentasi produk." },
                { title: "Higher", artist: "Tems", reason: "Vokal yang soulful dengan beat yang tenang memberikan kesan profesional dan fokus." }
            ]
        },
        'Edgy dan Berani': {
            captions: [
                "Rules are made to be broken. Tunjukkan sisi pemberontakmu dengan {product} dari {brand}. Dare to wear it?",
                "Bukan untuk semua orang. {product} dari {brand} ini dirancang bagi mereka yang berani tampil beda dan mendobrak batasan.",
                "Hitam bukan sekadar warna, tapi sebuah statement. {product} dari {brand} ini adalah kanvas untuk kepribadianmu yang kuat.",
            ],
            ctas: ["Unleash your inner rebel. Shop now.", "Limited stock. Get yours or regret later.", "Join the dark side. Link in bio."],
            songs: [
                { title: "Buka Pintu", artist: "Reality Club", reason: "Nuansa rock alternatif yang unik dan lirik yang 'gelap' cocok dengan vibe edgy." },
                { title: "Bad Guy", artist: "Billie Eilish", reason: "Beat yang minimalis namun 'dark' dan ikonik sangat identik dengan gaya edgy." },
                { title: "Do I Wanna Know?", artist: "Arctic Monkeys", reason: "Riff gitar yang ikonik dan nuansa rock yang 'cool' memberikan kesan pemberontak." }
            ]
        },
        'Minimalis dan Tenang': {
            captions: [
                "Less is more. Temukan keindahan dalam kesederhanaan dengan {product} dari {brand}. Esensi dari gaya yang tenang.",
                "Ketenangan dalam setiap helai. {product} dari {brand} ini menawarkan kenyamanan maksimal dengan palet warna netral yang menenangkan.",
                "Gaya yang bersih, pikiran yang jernih. {product} dari {brand} adalah pilihan tepat untuk Anda yang menghargai desain minimalis dan fungsional.",
            ],
            ctas: ["Discover our essentials collection.", "Sempurnakan gaya minimalis Anda. Klik link di bio.", "Tersedia dalam warna-warna bumi."],
            songs: [
                { title: "Rehat", artist: "Kunto Aji", reason: "Lirik yang menenangkan dan musik yang syahdu sangat cocok dengan tema minimalis." },
                { title: "Saturn", artist: "SZA", reason: "Alunan musik yang dreamy dan vokal yang lembut menciptakan suasana tenang." },
                { title: "Location", artist: "Khalid", reason: "Beat R&B yang laid-back dan modern memberikan kesan santai dan 'clean'." }
            ]
        },
        'Emosional dan Menyentuh': {
            captions: [
                "Pakaian bukan hanya tentang apa yang kita kenakan, tapi tentang apa yang kita rasakan. {product} dari {brand} ini dirancang untuk terasa seperti pelukan hangat, sebuah pengingat lembut bahwa Anda layak merasa nyaman menjadi diri sendiri.",
                "Setiap momen dalam hidup adalah sebuah cerita. Biarkan {product} dari {brand} ini menjadi bagian dari bab terindah dalam kisahmu. Kenakan saat tertawa, saat merenung, saat meraih mimpi. Ciptakan kenangan yang akan selalu melekat.",
                "Di tengah dunia yang serba cepat, ada kekuatan dalam kelembutan. {product} dari {brand} ini adalah undangan untuk berhenti sejenak, bernapas, dan merasakan. Rasakan setiap detailnya, dan biarkan ia menguatkan versi terbaik dari dirimu.",
            ],
            ctas: ["Temukan potongan yang mengerti Anda. Klik link di bio.", "Jadikan ini bagian dari ceritamu. Pesan sekarang.", "Bagikan satu kata tentang perasaanmu hari ini di kolom komentar."],
            songs: [
                { title: "Manusia Kuat", artist: "Tulus", reason: "Liriknya yang memberdayakan memberikan kekuatan dan sentuhan emosional yang mendalam." },
                { title: "Bertaut", artist: "Nadin Amizah", reason: "Melodi dan liriknya yang puitis menciptakan suasana haru dan koneksi batin." },
                { title: "Easy On Me", artist: "Adele", reason: "Lagu balada yang kuat tentang kerapuhan dan self-love, sangat menyentuh." }
            ]
        }
    };

    // --- FUNGSI UTAMA ---
    document.getElementById('generatorForm').addEventListener('submit', function(event) {
        event.preventDefault();

        const brandName = document.getElementById('brandName').value.trim();
        const tone = document.getElementById('tone').value;
        const resultsContainer = document.getElementById('results');
        
        let productDescription = document.getElementById('productDescription').value.trim();
        const productLink = document.getElementById('productLink').value.trim();
        const imageUploaded = document.getElementById('imageUpload').files.length > 0;

        let effectiveDescription = productDescription;

        if (!effectiveDescription && productLink) {
            effectiveDescription = `produk dari link ini: ${productLink}`;
        } else if (!effectiveDescription && !productLink && imageUploaded) {
            effectiveDescription = `produk yang terlihat pada gambar yang diunggah`;
        }
        
        if (!effectiveDescription) {
            alert('Harap isi salah satu informasi produk: Deskripsi, Link, atau Foto.');
            return;
        }

        const selectedTemplate = templates[tone];
        if (!selectedTemplate) return;

        resultsContainer.innerHTML = '';
        
        for (let i = 0; i < 2; i++) {
            const captionTmpl = getRandomItem(selectedTemplate.captions);
            const ctaTmpl = getRandomItem(selectedTemplate.ctas);
            const songTmpl = getRandomItem(selectedTemplate.songs);

            let finalCaption = captionTmpl.replace(/{product}/g, effectiveDescription).replace(/{brand}/g, brandName);
            finalCaption += `\n\n${ctaTmpl}`;
            
            const finalHashtags = generateHashtags(brandName, effectiveDescription);

            const card = document.createElement('div');
            card.className = 'result-card';
            
            const uniqueId = `caption-${i}`;
            card.innerHTML = `
                <button class="copy-btn" onclick="copyResultToClipboard('${uniqueId}')">Salin</button>
                <h3>Opsi Konten #${i + 1}</h3>
                <div id="${uniqueId}">
                    <p>${finalCaption}</p>
                    <p class="hashtags">${finalHashtags}</p>
                </div>
                <div class="song-recommendation">
                    <strong>Rekomendasi Lagu: ${songTmpl.title} - ${songTmpl.artist}</strong>
                    <em>Alasan: ${songTmpl.reason}</em>
                </div>
            `;
            
            resultsContainer.appendChild(card);
        }

        resultsContainer.classList.remove('hidden');
        resultsContainer.scrollIntoView({ behavior: 'smooth' });
    });

    // --- FUNGSI BANTUAN ---

    document.getElementById('imageUpload').addEventListener('change', function(event) {
        const previewContainer = document.getElementById('imagePreview');
        previewContainer.innerHTML = '';
        const file = event.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(e) {
                const img = document.createElement('img');
                img.src = e.target.result;
                previewContainer.appendChild(img);
            }
            reader.readAsDataURL(file);
        }
    });

    function getRandomItem(arr) {
        return arr[Math.floor(Math.random() * arr.length)];
    }

    function generateHashtags(brand, desc) {
        let tags = new Set();
        tags.add(`#${brand.replace(/\s+/g, '')}`);
        
        const words = desc.toLowerCase().replace(/[^a-z\s]/g, '').split(/\s+/);
        const keywords = ['kemeja', 'kaos', 'baju', 'dress', 'flanel', 'katun', 'ootd', 'fashion', 'style', 'outfit', 'link', 'gambar'];
        
        words.forEach(word => {
            if (keywords.includes(word) && tags.size < 6) {
                tags.add(`#${word}`);
            }
        });
        
        tags.add('#OOTDIndonesia');
        tags.add('#LocalBrand');
        
        return Array.from(tags).join(' ');
    }

    function copyResultToClipboard(elementId) {
        const element = document.getElementById(elementId);
        const textToCopy = element.innerText || element.textContent;
        
        navigator.clipboard.writeText(textToCopy.trim()).then(() => {
            const button = event.target;
            const originalText = button.textContent;
            button.textContent = 'Disalin!';
            button.style.backgroundColor = 'var(--success-color)';
            
            setTimeout(() => {
                button.textContent = originalText;
                button.style.backgroundColor = 'var(--secondary-color)';
            }, 2000);
        }).catch(err => {
            console.error('Gagal menyalin: ', err);
        });
    }
    </script>

</body>
</html>
