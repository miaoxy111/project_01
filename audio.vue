<template>
    <div>
        <audio :src="'http://39.103.217.204:80' + urlValue" style="opacity: 1" v-if="urlValue && urlValue != ''"
            :id="idValue"></audio>
        <span class="play_btn" @click="playAudio(idValue)" v-if="urlValue && urlValue != ''">播放录音</span>
    </div>
</template>

<script>
export default {
    data() {
        return {
            urlValue: '',
            idValue: ''
        };
    },
    created() {
        const urlParams = new URLSearchParams(window.location.search);
        this.urlValue = urlParams.get('url') || '';
        this.idValue = urlParams.get('id') || '';
    },
    methods: {
        playAudio(audioId) {
            const audio = document.getElementById(audioId);
            if (!audio) return;
            if (audio.paused) {
                document.querySelectorAll('audio').forEach(item => {
                    if (item.id !== audioId) item.pause();
                });
                audio.play();
            } else {
                audio.pause();
            }
        }
    }
}
</script>

<style scoped>
.play_btn {
    cursor: pointer;
    color: #409EFF;
}

.play_btn:hover {
    text-decoration: underline;
}
</style>