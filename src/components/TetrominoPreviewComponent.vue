<script lang="ts" setup>
import { defineProps, withDefaults } from 'vue';
import { Tetromino, TETROMINO_TYPE } from '../common/Tetromino';

interface Props {
    tetromino: Array<Array<number>>
}

const props = withDefaults(defineProps<Props>(), {
    tetromino: undefined,
})

const classPreviewBlockColor = (type: number) => {
    if (type === 0) return 'no-block';
    return Tetromino.id(type as TETROMINO_TYPE);
}
</script>

<template>
    <div class="tetromino-preview">
        <label>Next Block</label>
        <table class="field">
            <tr v-for="(row, y) in props.tetromino" :key="y">
                <td
                    class="block"
                    v-for="(col, x) in row"
                    :key="() => `${x}${y}`"
                    :class="classPreviewBlockColor(col)"
                >
                </td>
            </tr>
        </table>
    </div>
</template>

<style lang="scss" scoped>
.block {
  width: 1em;
  height: 1em;
  border: 0.1px solid #95a5a6;

  &-i {
    background: #3498db;
  }
  &-o {
    background: #f1c40f;
  }
  &-t {
    background: #9b59b6;
  }
  &-j {
    background: #1e3799;
  }
  &-l {
    background: #e67e22;
  }
  &-s {
    background: #2ecc71;
  }
  &-z {
    background: #e74c3c;
  }
}
.tetromino-preview {
  width: 6.5em;
  height: 5em;
  padding: 0.1em;

  border: solid 0.5px;

  .field {
    border-collapse: collapse;
    border: none;
    margin: 0px auto;

    .no-block {
      border: 0px none;
    }
  }
}
</style>