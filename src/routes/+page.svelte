<script>
  import Head from '$components/head.svelte'
  import ProjectCard from '$components/project-card.svelte'
  import {
    authorsStore,
    siteMetadataStore,
  } from '$stores/site-metadata'
  export let data

  const {
    siteUrl,
    name: siteName,
    description,
    openGraphDefaultImage,
  } = $siteMetadataStore || []
  const { name: authorName } = $authorsStore || []
</script>

<Head
  title={`${siteName} · ${authorName}`}
  {description}
  image={openGraphDefaultImage.url}
  url={`${siteUrl}`}
/>
<h1 class="font-bold mb-10 text-center text-5xl">
  Welcome to my Portfolio

</h1>

   
<div class="flex-none card mb-20 p-10  lg:flex bg-neutral">

<!--div class="realtive group card mb-20 p-10 shadow-2xl bg-neutral items-end"-->
<!--div class=" d-flex flex-column my-20 px-25 py-8 
bg-neutral "-->
<!--h1 class="font-bold text-center mb-20 text-5xl">
  Welcome to my Portfolio
</h1-->

{#each data.authors as { name, intro, picture: { url } }}
  <div class="flex mb-35 items-end">
    <div class="mr-b">
    

      <h2 class="text-base-100 text-3xl mb-6 font-bold tracking-wider">  {name} </h2>
      <p class="text-xl mb-5 mr-2">{intro}</p>
    </div>
    <img class="mask mask-circle h-52" src={url} alt={name} />
  </div>

{/each}
</div>
<div
  class="grid gap-10 md:grid-cols-4 md:px-10 lg:grid-cols-6 lg:-mx-52"
>
  {#each data.projects as { name, slug, description, image }}
    <ProjectCard {name} {description} url={image[0].url} {slug} />
  {/each}
</div>
