<script>
  import PageInfo from "$lib/components/PageInfo.svelte";
  import { _PAGE_TITLE } from "./+page";
  export let data;
</script>

<svelte:head>
  <PageInfo title={_PAGE_TITLE} />
</svelte:head>

<div class="posts">
  {#each data.pages as page}
    <a class="default post" href="/blog/{page.slug}">
      <p class="title">
        {page.attributes.title}
        <i class="date">
          {new Date(page.attributes.date).toLocaleDateString()}
        </i>
      </p>
      <p class="description">{page.attributes.description}</p>
    </a>
  {/each}
</div>

<style lang="scss">
  @use "$lib/style/constants.scss";
  @use "sass:color";

  .posts {
    display: flex;
    flex-direction: column;
    gap: 1em;
  }

  .post {
    display: block;
    background-color: color.adjust(constants.$dark, $lightness: 10%);
    padding: 8px 16px;
    border-radius: 4px;

    p {
      margin: 0;
    }

    p.title {
      font-weight: bold;
      font-size: 1.8em;
      display: block;
    }

    .date {
      font-weight: normal;
      font-size: small;
    }
  }
</style>
