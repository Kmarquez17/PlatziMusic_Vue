<template lang="pug">
  #app
    img(src='dist/logo.png')
    h1 PlatziMusic
    select(v-model="selectedCountry")
      option(v-for="country in countries" :value="country.value") {{country.name}}
    Spinner(v-show="loading")
    ul
      Artist(v-for="(artist) in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
</template>

<script>
import getArtists from './api/index';
import Artist from './components/Artist';
import Spinner from './components/Spinner';
export default {
	name: 'app',
	data() {
		return {
			artists: [],
			countries: [
				{ name: 'Argentina', value: 'argentina' },
				{ name: 'Colombia', value: 'colombia' },
				{ name: 'España', value: 'spain' },
				{ name: 'Nicaragua', value: 'nicaragua' },
			],
			selectedCountry: 'argentina',
			loading: true,
		};
	},
	components: {
		Artist,
		Spinner,
	},
	methods: {
		refreshArtists() {
			const self = this;
			self.loading = true;
			self.artists = [];
			getArtists(this.selectedCountry).then(function(artists) {
				self.loading = false;
				self.artists = artists;
			});
		},
	},
	mounted() {
		this.refreshArtists();
	},
	watch: {
		selectedCountry() {
			this.refreshArtists();
		},
	},
};
</script>

<style lang="stylus">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
  display: block;
}

a {
  color: #2c3e50;
  font-size: 18px;
  font-weight: 700;
  text-decoration: none;
}

select {
  width: 50%;
  font-family: Arial;
  font-weight: 700;
  height: 30px;
  border: none;
  background: transparent;
} 
</style>
