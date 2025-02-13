<script lang="ts">
  /* @ts-ignore */
  import SvgIcon from "@jamescoyle/svelte-icon/src/svg-icon.svelte";
  import { page } from "$app/stores";

  import { mdiGithub } from "@mdi/js";
  import schoolGithub from "$lib/assets/icons/schoolGithub.svgpath?raw";
  import discord from "$lib/assets/icons/discord.svgpath?raw";

  import { _PAGE_SUBTITLE, _PAGE_TITLE } from "./+layout";

  const LINKS = {
    "/": "About",
    "/blog/": "Blog",
  };
</script>

<svelte:head>
  <link rel="icon" href="/profile-image.png" />
</svelte:head>

<main>
  <header>
    <a href="/" class="backlink psm">
      <img
        class="pfp"
        src="/profile-image.png"
        alt="Avatar"
      />
      <div class="vbox">
        <h1>{_PAGE_TITLE}</h1>
        <em>{_PAGE_SUBTITLE}</em>
      </div>
    </a>
    <nav class="ps">
      {#each Object.entries(LINKS) as [url, name]}
        <a href={url} class={$page.url.pathname === url ? "selected" : ""}
          >{name}</a
        >
      {/each}
    </nav>
  </header>

  <div class="content ps">
    <slot />
  </div>

  <footer class="psm">
    <div class="ps">
      <div>
        <b>silver_volt4</b>
      </div>
      <div class="links">
        <a
          href="https://github.com/silver-volt4"
          target="_blank"
          data-tooltip="My GitHub profile"
        >
          <SvgIcon type="mdi" path={mdiGithub} size={32}></SvgIcon>
        </a>
        <a
          href="https://github.com/sykdan"
          target="_blank"
          data-tooltip="My school GitHub profile"
        >
          <SvgIcon type="mdi" path={schoolGithub} size={32}></SvgIcon>
        </a>
        <a
          href="https://discord.com/users/276742341031755776"
          target="_blank"
          data-tooltip="Discord"
        >
          <SvgIcon type="mdi" path={discord} size={32}></SvgIcon>
        </a>
      </div>
    </div>
  </footer>
</main>

<style lang="scss">
  @use "$lib/style/constants.scss";
  @use "sass:color";

  $darkBack: color.adjust(constants.$dark, $lightness: 3%);

  a.backlink {
    color: unset;
    text-decoration: unset;
    margin: 0;
    max-width: 1000px;
    padding: 32px 24px;
    margin: 0 auto;
  }

  header a.backlink,
  footer {
    display: flex;
    align-items: center;
    gap: 32px;
  }

  main {
    display: flex;
    flex-direction: column;
    min-height: 100vh;

    .content {
      flex-grow: 1;
      margin-bottom: 0;
    }
  }

  header {
    justify-content: center;
    margin-bottom: 32px;
    padding-bottom: 0;
    background-color: $darkBack;

    .vbox {
      display: flex;
      flex-direction: column;
    }

    nav {
      display: flex;
      padding: 0;
      margin-top: 0;
      margin-bottom: 0;

      a {
        flex: 1;
        display: block;
        font-size: 1.25em;
        color: constants.$light;
        text-decoration: none;
        padding: 4px;
        text-align: center;

        transition: background-color 0.1s;

        &:hover,
        &.selected:hover {
          background-color: color.adjust(constants.$light, $alpha: -0.8);
        }

        &.selected {
          background-color: color.adjust(constants.$light, $alpha: -0.9);
          border-bottom: solid 1px constants.$light;
        }
      }
    }

    h1 {
      display: inline-block;
      font-size: 48px;
      margin: 0;
    }

    .pfp {
      height: 128px;
      border-radius: 100%;
    }
  }

  footer {
    > div {
      padding-top: 32px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 32px;
    }
    background-color: $darkBack;
  }

  .links {
    display: flex;
    gap: 8px;
    a {
      background: none;
      border: none;
      display: inline;
      padding: 0;
      color: constants.$light;
    }
  }

  @media screen and (max-width: 600px) {
    header {
      a.backlink {
        gap: 16px;
        padding: 32px 16px;
      }

      h1 {
        font-size: 32px;
      }

      img.pfp {
        height: 96px;
      }
    }
  }
</style>
