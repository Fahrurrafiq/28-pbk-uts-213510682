<template>
	<div>
	  <h1>Daftar Kegiatan</h1>
	  <input type="text" v-model="inputKegiatan" placeholder="Tambahkan kegiatan" />
	  <button @click="tambahKegiatan">Tambahkan</button>
	  <br /><br />
	  <input type="checkbox" id="checkbox-filter" v-model="showIncomplete"> Tampilkan yang belum selesai
	  <br /><br />
	  <ul>
		<li v-for="(kegiatan, index) in filteredKegiatan" :key="index" :class="{ 'button-hidden': kegiatan.completed }">
		  <input type="checkbox" v-model="kegiatan.completed" @change="toggleKegiatan(kegiatan)" />
		  <span :class="{ 'line-through': kegiatan.completed }">{{ kegiatan.nama }}</span>
		  <button @click="hapusKegiatan(kegiatan)">Hapus</button>
		</li>
	  </ul>
	</div>
  </template>
  
  <script>
  export default {
	data() {
	  return {
		inputKegiatan: '',
		showIncomplete: false,
		kegiatan: []
	  };
	},
	computed: {
	  filteredKegiatan() {
		if (this.showIncomplete) {
		  return this.kegiatan.filter(kegiatan => !kegiatan.completed);
		} else {
		  return this.kegiatan;
		}
	  }
	},
	methods: {
	  tambahKegiatan() {
		if (this.inputKegiatan !== '') {
		  this.kegiatan.push({
			nama: this.inputKegiatan,
			completed: false
		  });
		  this.inputKegiatan = '';
		}
	  },
	  toggleKegiatan(kegiatan) {
		kegiatan.completed = !kegiatan.completed;
	  },
	  hapusKegiatan(kegiatan) {
		const index = this.kegiatan.indexOf(kegiatan);
		if (index > -1) {
		  this.kegiatan.splice(index, 1);
		}
	  }
	}
  };
  </script>
  
  <style scoped>
  body {
	font-family: 'Roboto', sans-serif;
	background-color: #f8f8f8;
	margin: 0;
	padding: 0;
  }
  
  h1 {
	font-size: 36px;
	text-align: center;
	color: #333;
	margin-top: 20px;
	margin-bottom: 40px;
  }
  
  input[type="text"] {
	padding: 10px;
	font-size: 18px;
	border-radius: 5px;
	border: 2px solid #ccc;
	margin-right: 10px;
  }
  
  button {
	padding: 10px 20px;
	font-size: 18px;
	border-radius: 5px;
	border: none;
	background-color: #008CBA;
	color: #fff;
	cursor: pointer;
  }
  
  button:hover {
	background-color: #006C9D;
  }
  
  input[type="checkbox"] {
	margin-right: 5px;
	cursor: pointer;
  }
  
  ul {
	list-style: none;
	padding: 0;
  }
  
  li {
	margin-bottom: 10px;
	display: flex;
	align-items: center;
	background-color: #fff;
	padding: 15px;
	border-radius: 5px;
	box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  }
  
  li span {
	margin-left: 20px;
	font-size: 20px;
	color: #333;
	flex-grow: 1;
  }
  
  li button {
	padding: 10px 15px;
	font-size: 16px;
	border-radius: 5px;
	border: none;
	background-color: #f44336;
	color: #fff;
	cursor: pointer;
	margin-left: 20px;
  }
  
  li button:hover {
	background-color: #d32f2f;
  }
  
  .button-hidden button {
	display: none;
  }
  
  li span.line-through {
	text-decoration: line-through;
	color: #999;
  }
  </style>
  