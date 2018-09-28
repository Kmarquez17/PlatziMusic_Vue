<template lang="pug">
  li
    h2: a(:href="artist.url"  target="_blank") {{artist.name}}
    img(:src="artist.image[2]['#text']")
</template>

<script>
export default {
	name: 'artist',
	props: ['artist'],
};
</script>

<style lang="stylus" scoped>
li {
    display: inline-block;
    margin: 10px 10px;
    box-shadow: 0.7px 0.7px 10px #2c3e50;
    padding: 25px;
    border-radius: 5%;
}
</style>
