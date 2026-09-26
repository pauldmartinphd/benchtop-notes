# Fonts

## Font Rendering Configuration

### 1. Freetype2 Symlinks
Create symlinks for good-looking rendering defaults:

    ln -s /etc/fonts/conf.avail/11-lcdfilter-default.conf /etc/fonts/conf.d
    ln -s /etc/fonts/conf.avail/10-hinting-slight.conf /etc/fonts/conf.d

### 2. Fontconfig: /etc/fonts/local.conf

Default font families:

* serif → Heuristica
* sans-serif → Noto Sans, Noto Sans CJK SC
* monospace → Liberation Mono, Noto Sans Mono CJK SC
* fantasy → Signika
* cursive → TeX Gyre Chorus

The imported XML had missing opening and closing tags. The complete example below retains its family mappings, including entries omitted from the earlier summary. `Corberl` and `SegoeUI` are corrected to `Corbel` and `Segoe UI`. These are selected substitutions; they are not a claim of metric compatibility with every original face.

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <alias>
    <family>serif</family>
    <prefer>
      <family>Heuristica</family>
    </prefer>
  </alias>
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>Noto Sans</family>
      <family>Noto Sans CJK SC</family>
    </prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer>
      <family>Liberation Mono</family>
      <family>Noto Sans Mono CJK SC</family>
    </prefer>
  </alias>
  <alias>
    <family>fantasy</family>
    <prefer>
      <family>Signika</family>
    </prefer>
  </alias>
  <alias>
    <family>cursive</family>
    <prefer>
      <family>TeX Gyre Chorus</family>
    </prefer>
  </alias>
  <match target="pattern">
    <test name="family"><string>Arial</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Liberation Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Arial Narrow</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Liberation Sans Narrow</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Book Antiqua</string></test>
    <edit name="family" mode="assign" binding="strong"><string>TeX Gyre Bonum</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Calibri</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Carlito</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Cambria</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Caladea</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>New Century Schoolbook</string></test>
    <edit name="family" mode="assign" binding="strong"><string>TeX Gyre Schola</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Comic Sans MS</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Signika</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Consolas</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Droid Sans Mono Slashed</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Constantia</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Merriweather</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Corbel</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Merriweather Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Courier New</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Courier Prime</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Geneva</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Noto Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Georgia</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Gelasio</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Helvetica</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Liberation Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Helvetica Narrow</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Liberation Sans Narrow</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Helvetica Neue</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Open Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Impact</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Oswald</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>ITC Zapf Chancery</string></test>
    <edit name="family" mode="assign" binding="strong"><string>TeX Gyre Chorus</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Calligraphy</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Quintessential</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Handwriting</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Quintessential</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Casual</string></test>
    <edit name="family" mode="assign" binding="strong"><string>CantoraOne</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Console</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Droid Sans Mono</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Sans Typewriter</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Liberation Sans Mono</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Fax</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Luxi Mono</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Sans</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Droid Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Lucida Grande</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Droid Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Palatino Linotype</string></test>
    <edit name="family" mode="assign" binding="strong"><string>TeX Gyre Pagella</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Segoe UI</string></test>
    <edit name="family" mode="assign" binding="strong"><string>WeblySleek UI</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Symbol</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Symbola</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Tahoma</string></test>
    <edit name="family" mode="assign" binding="strong"><string>DejaVu Sans Condensed</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Times New Roman</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Liberation Serif</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Trebuchet MS</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Ubuntu</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Verdana</string></test>
    <edit name="family" mode="assign" binding="strong"><string>DejaVu Sans</string></edit>
  </match>
  <match target="pattern">
    <test name="family"><string>Wingdings</string></test>
    <edit name="family" mode="assign" binding="strong"><string>Symbola</string></edit>
  </match>
</fontconfig>
```

### 3. Install Distro Fonts

    zypper in google-noto-fonts
    zypper in texlive-tex-gyre-fonts

### 4. Font package references

The names below were collected from multiple distributions, including Arch/AUR. They identify fonts to locate and package; they are not an openSUSE installation command.

* Caladea (ttf-caladea)
* Carlito (ttf-carlito)
* DejaVu (ttf-dejavu)
* Impallari Cantora (aur/ttf-impallari-cantora)
* Liberation (ttf-liberation)
* Noto (noto-fonts)
* Open Sans (ttf-opensans)
* Overpass (otf-overpass)
* Roboto (ttf-roboto)
* TeX Gyre (tex-gyre-fonts)
* Ubuntu (ttf-ubuntu-font-family)
* Courier Prime (aur/ttf-courier-prime)
* Gelasio (aur/ttf-gelasio-ib)
* Merriweather (aur/ttf-merriweather)
* Source Sans Pro (aur/ttf-source-sans-pro-ibx)
* Signika (aur/ttf-signika)

### 5. Envision Settings
[Reddit](https://www.reddit.com/r/linux/comments/1bh1x80/tweaks_for_the_freetype_font_rendering/) / [GitHub](https://github.com/maximilionus/freetype-envision)

## Open Source Font Stack (Curated)

* Atkinson Hyperlegible (accessibility)
* Fira
* GNU Unifont
* Google Noto (universal coverage)
* Hack Pro
* IBM Plex
* Intel One Mono
* Inter
* JetBrains Mono
* Microsoft Cascadia Code
* NebulaSans (from the original font list)
* Ubuntu

## Other font questions

The original vision also called for ClearType-style rendering, Microsoft TTF support, and Microsoft-compatible defaults for office documents. These remain evaluation questions alongside the substitution configuration.

## Infinality Font Rendering
Infinality and Infinality Remix were earlier candidates. Keep their references for comparison, but verify compatibility before using old FreeType patches. The working configuration above uses Fontconfig settings; freetype-envision remains an option to evaluate.

* https://github.com/pdeljanov/infinality-remix/issues/13
* https://github.com/pdeljanov/infinality-remix

## Reference Links

* https://news.ycombinator.com/item?id=30705078
* https://gist.github.com/cryzed/e002e7057435f02cc7894b9e748c5671
* https://wiki.archlinux.org/title/Font_configuration
