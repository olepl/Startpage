<script>
    const themes = [
        { "class": "light",     "icon": "far fa-sun"    },
        { "class": "dark",      "icon": "far fa-moon"   },
        { "class": "neon",      "icon": "fas fa-bolt"   }
    ]
    
    // load theme or set to default
    let theme = localStorage.getItem('theme') !== null? JSON.parse(localStorage.getItem('theme')) : themes[0];
    localStorage.setItem('theme', JSON.stringify(theme));
    
    // initial apply theme
    let icon = theme.icon;
    document.body.classList.add('theme');
    document.body.classList.add(theme.class);

    // set index to corresponding place in 'themes', or to -1 if not in there
    let index = -1;
    for (let i in themes) {
        if (themes[i].class == theme.class) { index = i; break; }
    }

    function apply_theme() {
        for (let i in themes) { document.body.classList.remove(themes[i].class); } // clear previous theme

        icon = theme.icon;
        document.body.classList.add(theme.class);
    }

    function switch_theme() {
        theme = themes[++index % themes.length]; // cycle between themes
        localStorage.setItem('theme', JSON.stringify(theme));

        apply_theme();
    };
</script>

<div on:click="{switch_theme}" id="theme_button">
    <i class={icon}></i>
</div>

<style>
    #theme_button {
        position: absolute;
        top: 0;
        right: 0;
        margin: 1em;

        width: 2.5em;
        height: 2.5em;

        display: flex;
        align-items: center;
        justify-content: center;

        border-radius: 50%;
    }
    #theme_button:hover {
        background-color: var(--sbg);
    }

    #theme_button > i {
        font-size: 1.5em;
    }
</style>
