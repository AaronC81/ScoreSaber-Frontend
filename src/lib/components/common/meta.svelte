<script lang="ts">
   export let image: string = 'https://novus.scoresaber.com/512x512.png';
   export let title: string = 'ScoreSaber';
   export let description: string = 'ScoreSaber';
   export let url: string = 'https://scoresaber.com';
   let descriptionTag = `<meta property="og:description" content="${description}" />`;
</script>

<meta property="og:image" content={image} />
<meta property="og:image:secure_url" content={title} />
<meta property="og:title" content={title} />
{@html descriptionTag}
<meta property="og:type" content="website" />
<meta property="og:url" content={url} />
<meta property="og:site_name" content="ScoreSaber" />
