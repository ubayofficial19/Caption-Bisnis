<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fashion Post - Prompt Generator</title>
    <style>
        /* CSS untuk tampilan yang modern dan responsif */
        :root {
            --primary-color: #007bff;
            --secondary-color: #6c757d;
            --background-color: #f8f9fa;
            --surface-color: #ffffff;
            --text-color: #212529;
            --border-color: #dee2e6;
            --success-color: #28a745;
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
            box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.2);
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

        .button-group {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap; /* Agar tombol bisa turun jika layar sempit */
        }

        .submit-btn, .secondary-btn {
            flex: 1 1 200px; /* Tombol bisa membesar dan mengecil */
            padding: 0.85rem;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s, transform 0.1s;
        }

        .submit-btn {
            background-color: var(--primary-color);
        }

        .submit-btn:hover {
            background-color: #0056b3;
        }
        
        .submit-btn:active, .secondary-btn:active {
            transform: scale(0.99);
        }
        
        .secondary-btn {
            background-color: var(--secondary-color);
        }

        .secondary-btn:hover {
            background-color: #5a6268;
        }

        #results {
            margin-top: 2.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid var(--border-color);
        }

        .hidden {
            display: none;
        }

        .result-box {
            margin-bottom: 2rem;
        }

        h2 {
            color: var(--text-color);
            margin-bottom: 1rem;
        }

        pre {
            background-color: #e9ecef;
            padding: 1rem;
            padding-top: 3.5rem; /* Memberi ruang untuk tombol di atas */
            border-radius: 8px;
            white-space: pre-wrap;
            word-wrap: break-word;
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.95rem;
            position: relative;
        }
        
        .button-container {
            position: absolute;
            top: 10px;
            right: 10px;
            display: flex;
            gap: 8px;
        }

        .copy-btn, .run-ai-btn {
            padding: 0.4rem 0.8rem;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.8rem;
            font-weight: 500;
            transition: background-color 0.2s;
        }

        .copy-btn {
            background-color: var(--secondary-color);
        }
        .copy-btn:hover {
            background-color: #5a6268;
        }
        
        .run-ai-btn {
            background-color: var(--primary-color);
        }
        .run-ai-btn:hover {
            background-color: #0056b3;
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
            <h1>Fashion Post Prompt Generator</h1>
            <p>Buat prompt AI yang sempurna untuk caption & lagu postingan baju Anda.</p>
        </header>

        <form id="promptForm">
            <div class="form-group">
                <label for="brandName">Nama Brand / Usaha Anda</label>
                <input type="text" id="brandName" placeholder="Contoh: UrbanStyle ID" required>
            </div>

            <div class="form-group">
                <label for="targetAudience">Siapa Target Audiens Anda?</label>
                <input type="text" id="targetAudience" placeholder="Contoh: Mahasiswa & pekerja muda, usia 18-28 tahun" required>
            </div>

            <fieldset style="border:1px solid var(--border-color); padding: 1rem; border-radius: 8px; margin-bottom: 1.5rem;">
                <legend style="padding: 0 0.5rem; font-weight: 600;">Informasi Produk Baju</legend>
                
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
                    <textarea id="productDescription" rows="4" placeholder="Contoh: Kemeja flanel lengan panjang, motif kotak-kotak warna biru navy dan putih, bahan katun premium yang lembut."></textarea>
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
                </select>
            </div>
            
            <!-- KONTROL TOMBOL BARU -->
            <div class="button-group">
                <button type="submit" class="submit-btn">Buat Prompt!</button>
                <button type="button" id="generateRandomBtn" class="secondary-btn">Isi Contoh Acak</button>
            </div>
        </form>

        <div id="results" class="hidden">
            <div class="result-box">
                <h2>1. Prompt untuk Caption</h2>
                <pre>
                    <div class="button-container">
                        <button class="run-ai-btn" onclick="openInAI('captionPromptOutput')">Buka di Gemini</button>
                        <button class="copy-btn" onclick="copyToClipboard('captionPromptOutput')">Salin</button>
                    </div>
                    <code id="captionPromptOutput"></code>
                </pre>
            </div>
            <div class="result-box">
                <h2>2. Prompt untuk Rekomendasi Lagu</h2>
                <pre>
                    <div class="button-container">
                        <button class="run-ai-btn" onclick="openInAI('songPromptOutput')">Buka di Gemini</button>
                        <button class="copy-btn" onclick="copyToClipboard('songPromptOutput')">Salin</button>
                    </div>
                    <code id="songPromptOutput"></code>
                </pre>
            </div>
        </div>
    </div>

    <script>
        // JavaScript untuk fungsionalitas halaman
        document.getElementById('promptForm').addEventListener('submit', function(event) {
            event.preventDefault(); // Mencegah form mengirim data dan me-reload halaman

            // 1. Mengambil semua nilai dari input
            const brandName = document.getElementById('brandName').value.trim();
            const targetAudience = document.getElementById('targetAudience').value.trim();
            const productLink = document.getElementById('productLink').value.trim();
            const productDescription = document.getElementById('productDescription').value.trim();
            const imageUploaded = document.getElementById('imageUpload').files.length > 0;
            const tone = document.getElementById('tone').value;

            // Validasi dasar: setidaknya salah satu info produk harus diisi
            if (!productLink && !productDescription && !imageUploaded) {
                alert('Harap isi salah satu informasi produk: Upload foto, Link produk, atau Deskripsi.');
                return;
            }

            // 2. Membangun bagian informasi produk untuk prompt
            let productInfoText = '';
            if (productLink) {
                productInfoText = `Produk ini dapat dilihat detailnya pada link berikut: ${productLink}. Tolong analisis informasi dari link tersebut (nama produk, bahan, harga jika ada) untuk memperkaya caption.`;
            } else if (productDescription) {
                productInfoText = `Berikut adalah deskripsi produknya: "${productDescription}".`;
            } else if (imageUploaded) {
                productInfoText = `Produknya adalah baju yang ada di dalam gambar yang diunggah. Deskripsikan secara visual apa yang kamu lihat (warna, model, gaya, motif jika ada) dan gunakan deskripsi itu sebagai dasar caption.`;
            }

            // 3. Membuat template prompt untuk caption
            const captionPrompt = `Anda adalah seorang social media manager profesional untuk sebuah brand fashion.
Tugas Anda adalah membuat 3 opsi caption menarik untuk postingan Instagram.

Berikut adalah detailnya:
- Nama Brand: ${brandName}
- Target Audiens: ${targetAudience}
- Informasi Produk: ${productInfoText}
- Gaya Bahasa/Vibe yang Diinginkan: ${tone}

Instruksi Pembuatan Caption:
1. Buat 3 (tiga) alternatif caption yang berbeda.
2. Setiap caption harus memiliki hook (kalimat pembuka) yang kuat untuk menarik perhatian.
3. Sertakan call-to-action (CTA) yang jelas di akhir setiap caption (Contoh: "Klik link di bio!", "Shop now!", "Komen di bawah!").
4. Tambahkan 5-7 hashtag yang relevan dan spesifik di akhir setiap caption. Hashtag harus mencakup nama brand, jenis produk, dan audiens.
5. Pastikan gaya bahasa sesuai dengan vibe "${tone}" yang diminta.`;

            // 4. Membuat template prompt untuk rekomendasi lagu
            const songPrompt = `Anda adalah seorang music curator yang ahli dalam memilih lagu untuk konten media sosial.
Tugas Anda adalah merekomendasikan 3 lagu yang cocok untuk video/reels Instagram yang mempromosikan produk fashion.

Berikut adalah konteksnya:
- Brand: ${brandName}
- Target Audiens: ${targetAudience}
- Deskripsi Produk: ${productDescription || "Baju fashion yang stylish (detail ada pada link/gambar yang disediakan di prompt lain)."}
- Vibe yang Diinginkan: ${tone}

Instruksi Pemilihan Lagu:
1. Berikan 3 (tiga) rekomendasi lagu.
2. Untuk setiap lagu, sebutkan Judul Lagu dan Nama Artisnya.
3. Berikan alasan singkat (1-2 kalimat) mengapa lagu tersebut cocok dengan produk dan vibe yang diinginkan.
4. Pilih lagu yang sedang tren atau memiliki nuansa yang pas, bisa dari artis Indonesia maupun internasional.`;

            // 5. Menampilkan hasil prompt di halaman
            document.getElementById('captionPromptOutput').textContent = captionPrompt.trim();
            document.getElementById('songPromptOutput').textContent = songPrompt.trim();
            document.getElementById('results').classList.remove('hidden');
            
            // Scroll ke hasil agar terlihat
            document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
        });

        // Fungsi untuk menampilkan preview gambar yang diupload
        document.getElementById('imageUpload').addEventListener('change', function(event) {
            const previewContainer = document.getElementById('imagePreview');
            previewContainer.innerHTML = ''; // Kosongkan preview sebelumnya
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

        // Fungsi untuk menyalin teks ke clipboard
        function copyToClipboard(elementId) {
            const textToCopy = document.getElementById(elementId).textContent;
            navigator.clipboard.writeText(textToCopy).then(() => {
                // Beri feedback ke user bahwa teks berhasil disalin
                const button = event.target;
                const originalText = button.textContent;
                button.textContent = 'Disalin!';
                button.style.backgroundColor = 'var(--success-color)';
                
                setTimeout(() => {
                    button.textContent = originalText;
                    button.style.backgroundColor = 'var(--secondary-color)';
                }, 2000);

            }).catch(err => {
                console.error('Gagal menyalin teks: ', err);
                alert('Gagal menyalin teks.');
            });
        }

        /**
         * FUNGSI BARU: Membuka prompt di Google Gemini
         * @param {string} elementId - ID dari elemen <code> yang berisi teks prompt.
         */
        function openInAI(elementId) {
            // 1. Ambil teks prompt dari elemen yang sesuai.
            const promptText = document.getElementById(elementId).textContent;
            
            // 2. Encode teks prompt agar aman digunakan dalam URL.
            const encodedPrompt = encodeURIComponent(promptText);
            
            // 3. Buat URL untuk Google Gemini dengan prompt yang sudah di-encode.
            const geminiUrl = `https://gemini.google.com/app?prompt=${encodedPrompt}`;
            
            // 4. Buka URL tersebut di tab browser baru.
            window.open(geminiUrl, '_blank');
        }

        // --- FITUR BARU: GENERATE CONTOH ACAK ---

        /**
         * Fungsi untuk mengisi form dengan data acak dan men-trigger submit.
         */
        function generateRandomExample() {
            // 1. Data contoh untuk diisi secara acak
            const sampleBrands = ["Gaya Nusantara", "Urban Chic ID", "Kain Tenun Co.", "Streetwear Jakarta", "Ethereal Wear"];
            const sampleAudiences = ["Anak muda Gen Z yang suka fashion lokal & edgy", "Wanita karir usia 25-40 tahun yang elegan", "Pecinta budaya dan kain tradisional", "Mahasiswa yang aktif dan dinamis", "Remaja yang mengikuti tren Korea"];
            const sampleDescriptions = [
                "T-shirt oversized dengan sablon grafis peta Indonesia di bagian belakang, bahan katun combed 24s yang adem dan nyaman.",
                "Blazer wanita model crop top warna beige, bahan linen premium, dilengkapi kancing batok kelapa, cocok untuk acara formal dan kasual.",
                "Kemeja batik lengan pendek dengan motif parang modern, kombinasi warna sogan dan indigo, bahan katun primisima yang halus.",
                "Hoodie dengan tali serut tebal dan saku kanguru, warna hitam pekat, logo brand minimalis di dada kiri, bahan fleece tebal.",
                "Rok mini model plisket (pleated skirt) warna pastel ala Korea, bahan high-quality polyester yang tidak mudah kusut."
            ];
            const toneOptions = document.getElementById('tone').options;

            // 2. Fungsi bantuan untuk mendapatkan item acak dari sebuah array
            const getRandomItem = (arr) => arr[Math.floor(Math.random() * arr.length)];

            // 3. Mengambil elemen-elemen form
            const brandNameInput = document.getElementById('brandName');
            const audienceInput = document.getElementById('targetAudience');
            const descriptionInput = document.getElementById('productDescription');
            const toneSelect = document.getElementById('tone');
            const productLinkInput = document.getElementById('productLink');
            const imageUploadInput = document.getElementById('imageUpload');
            const imagePreview = document.getElementById('imagePreview');

            // 4. Mengosongkan input info produk lainnya untuk memastikan hanya deskripsi yang dipakai
            productLinkInput.value = '';
            imageUploadInput.value = ''; // Mengosongkan file input
            imagePreview.innerHTML = ''; // Menghapus preview gambar

            // 5. Mengisi form dengan data acak
            brandNameInput.value = getRandomItem(sampleBrands);
            audienceInput.value = getRandomItem(sampleAudiences);
            descriptionInput.value = getRandomItem(sampleDescriptions);
            toneSelect.selectedIndex = Math.floor(Math.random() * toneOptions.length);
            
            // 6. Memicu (trigger) event 'submit' pada form untuk menjalankan logika pembuatan prompt
            document.getElementById('promptForm').dispatchEvent(new Event('submit', { bubbles: true, cancelable: true }));
        }

        // Menambahkan event listener ke tombol baru
        document.getElementById('generateRandomBtn').addEventListener('click', generateRandomExample);

    </script>

</body>
</html>
