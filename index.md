const browser = await puppeteer.launch({
  args: ['--no-sandbox', '--disable-setuid-sandbox'],
});
sudo sysctl -w kernel.unprivileged_userns_clone=1
# cd to the downloaded instance
cd <project-dir-path>/node_modules/puppeteer/.local-chromium/linux-<revision>/chrome-linux/
sudo chown root:root chrome_sandbox
sudo chmod 4755 chrome_sandbox
# copy sandbox executable to a shared location
sudo cp -p chrome_sandbox /usr/local/sbin/chrome-devel-sandbox
# export CHROME_DEVEL_SANDBOX env variable
export CHROME_DEVEL_SANDBOX=/usr/local/sbin/chrome-devel-sandbox
export CHROME_DEVEL_SANDBOX=/usr/local/sbin/chrome-devel-sandbox
bahasa : free
layanan : xvfb

# Di seluruh file ini, versi `node_js` berikut digunakan:
#
# - free: '10' # Versi pemeliharaan LTS.
# - free: '12' # Versi LTS aktif mayor tertua.
# - free: '14' # Versi LTS aktif utama terbaru.

pekerjaan :
  termasuk :
    - os : ' osx '
      nama : ' Tes unit: macOS/Chromium '
      node_js : ' 10 '  # Versi pemeliharaan LTS.
      osx_image : xcode11.4
      env :
        - CHROMIUM = benar
      sebelum_instal :
        - PUPPETEER_PRODUCT=instal firefox npm
      naskah :
        - ls .local-chromium .local-firefox
        - npm jalankan tsc
        - npm menjalankan unit

    - os : ' jendela '
      nama : ' Tes unit: Windows/Chromium '
      node_js : ' 10 '  # Versi pemeliharaan LTS.
      env :
        - CHROMIUM = benar
      sebelum_instal :
        - PUPPETEER_PRODUCT=instal firefox npm
      naskah :
        - ls .local-chromium .local-firefox
        - npm jalankan tsc
        - travis_retry npm menjalankan unit

    # Modul fs.promises Node <10.17 bersifat eksperimental dan tidak berperilaku seperti
    # diharapkan. Masalah ini telah diperbaiki di Node 10.19, tetapi kami menjalankan unit test
    # hingga 10.15 untuk memastikan kami tidak menyebabkan regresi apa pun saat menggunakan
    # fs.janji. Lihat https://github.com/puppeteer/puppeteer/issues/6548 untuk
    # contoh.
    - node_js : ' 10.15.0 '
      nama : ' Node 10.15 Tes unit: Linux/Chromium '
      env :
        - CHROMIUM = benar
      sebelum_instal :
        - PUPPETEER_PRODUCT=instal firefox npm
      naskah :
        - npm menjalankan unit

    - node_js : ' 10 '  # Versi pemeliharaan LTS.
      name : ' Tes unit [dengan cakupan]: Linux/Chromium '
      env :
        - CHROMIUM = benar
      sebelum_instal :
        - PUPPETEER_PRODUCT=instal firefox npm
      naskah :
        - travis_retry npm jalankan unit-with-coverage
        - npm jalankan assert-unit-coverage

    - node_js : ' 12 '  # Versi LTS aktif mayor tertua.
      nama : ' Tes unit [Node 12]: Linux/Chromium '
      env :
        - CHROMIUM = benar
      sebelum_instal :
        - PUPPETEER_PRODUCT=instal firefox npm
      naskah :
        - npm menjalankan unit

    - node_js : ' 14 '  # Versi LTS aktif utama terbaru.
      nama : ' Tes unit [Node 14]: Linux/Chromium '
      env :
        - CHROMIUM = benar
      sebelum_instal :
        - PUPPETEER_PRODUCT=instal firefox npm
      naskah :
        - npm menjalankan unit

    - node_js : ' 12 '  # Versi LTS aktif mayor tertua.
      nama : ' Tes browser: Linux/Chromium '
      tambahan :
        krom : stabil
      env :
        - CHROMIUM = benar
      naskah :
        - npm menjalankan browser uji

    # Bot ini menjalankan semua pemeriksaan tambahan yang bukan merupakan pengujian unit Dalang utama.
    - node_js : ' 10 '  # Versi pemeliharaan LTS.
      nama : ' Tes tambahan: Linux/Chromium '
      env :
        - CHROMIUM = benar
      naskah :
        - npm menjalankan lint
        # Pastikan kami dapat membuat dokumen baru tanpa kesalahan
        - npm jalankan generate-docs
        - npm jalankan pastikan-benar-devtools-protokol-revisi

    # Bot ini berjalan secara terpisah saat mengubah package.json untuk menguji dalang-core
    # dan kami tidak ingin itu bocor ke bot lain dan menyebabkan masalah.
    - node_js : ' 10 '  # Versi pemeliharaan LTS.
      name : ' Uji bundling dan instal paket '
      env :
        - CHROMIUM = benar
      naskah :
        - npm jalankan uji-instal

    - node_js : ' 10 '  # Versi pemeliharaan LTS.
      nama : ' Uji coba unit: Linux/Firefox '
      env :
        - FIREFOX = true
      sebelum_instal :
        - PUPPETEER_PRODUCT=instal firefox npm
      naskah :
        - npm menjalankan funit

pemberitahuan :
  email : real
