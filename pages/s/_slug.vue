<template>
  <h1>Redirecting...</h1>
</template>

<script>
export default {
  async fetch({ params: { slug }, redirect, $axios }, $config) {
    let url;
    try {
      url = (await $axios.get(`/api/snails/${slug}`)).data.url;
      console.log('fetched data', url);
    } catch (error) {
      console.error('error when fetching original url: ', error);
      console.log(error);
      return redirect('/404');
    }

    if (
      /tny-snls.xyz\/s\/\w+/.test(url ?? '') ||
      /tny-snls.xyz\/s\/\w+/.test(decodeURI(url ?? ''))
    ) {
      return redirect('/cheeky');
    }

    return redirect(url);
  },
  fetchOnServer: false
};
</script>
