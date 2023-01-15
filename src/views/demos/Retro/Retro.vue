<template>
     <CodeSample code="import { ImageMagick } from '@imagemagick/magick-wasm/image-magick'

const canvas = document.getElementById('canvasId')

ImageMagick.readFromCanvas(canvas, (image) => {
    image.resize(320, 240);
    image.sigmoidalContrast(0, 8, 0.5);  // 0: _sharpen flag
    image.modulate(new Percentage(100), new Percentage(200), 
                   new Percentage(100));
    // -ordered-dither 4x4,8,8,8 
    // +dither -map palette.png
    image.filterType = FilterType.Point;
    image.resize(new MagickGeometry('200%'));
    image.writeToCanvas(canvas)
})" />

    <h3>.rotate(degrees: number)</h3>

    <div class="argument">
        <!-- label>Degrees:</label><input type="number" v-model="degrees" /  -->
    </div>
    <button :onclick="showExample">Execute</button>
    <hr/>
    <CodeSample code="// magick convert -resize 320x240 +sigmoidal-contrast 8,50% -modulate 100,200,100 -ordered-dither 4x4,8,8,8 +dither -map palette.png -sample 200% input.jpg output.png" />
    <CodeSample code="magick convert -resize 320x240 +sigmoidal-contrast 8,50% -modulate 100,200,100 -sample 200% input.jpg output.png" />
    <small> &copy; https://dailyportalz.jp/kiji/retro_PC_game-mitaina-shashin </small>
</template>

<script lang="ts">
import { IMagickImage, FilterType, MagickGeometry, Percentage } from '@imagemagick/magick-wasm'
import { MagickExample } from '@/magick-example'
import { Options, Vue } from 'vue-class-component'
import CodeSample from '@/components/CodeSample.vue'

@Options({
    emits: ["show-example"],
    components: {
        CodeSample,
    },
})
export default class Retro extends Vue implements MagickExample {

    showExample(): void { this.$emit('show-example', this) }

    changeImage(image: IMagickImage): void {
        image.resize(320, 240);
        image.sigmoidalContrast(0, 8, 0.5);  // 0: _sharpen flag
        image.modulate(new Percentage(100), new Percentage(200),
                           new Percentage(100));
        // -ordered-dither 4x4,8,8,8
        // +dither -map palette.png
        image.filterType = FilterType.Point;
        image.resize(new MagickGeometry('200%'));
    }
}
</script>
