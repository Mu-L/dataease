<template>
  <el-row>
    <el-col :span="24">
      <div class="filter-field">
        <div class="field-content">

          <div class="field-content-right">
            <el-row style="display:flex;height: 32px;">
              <draggable
                v-model="element.options.attrs.dragItems"
                group="dimension"
                animation="300"
                :move="onMove"
                class="theme-drag"
                style="width:100%;height: 100%;margin:0 10px;border-radius: 4px;overflow-x: auto;display: flex;align-items: center;"
                @end="end2"
              >
                <div class="list-group-container">
                  <drag-item
                    v-for="(item,index) in element.options.attrs.dragItems"
                    :key="item.id"
                    :item="item"
                    :index="index"
                    @closeItem="closeItem"
                  />
                </div>
                <transition-group class="list-group" :data-value="$t('panel.drag_here')" />
              </draggable>
            </el-row>
          </div>
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<script>
import draggable from 'vuedraggable'
import DragItem from '@/components/DragItem'
export default {
  name: 'FilterHead',
  components: {
    draggable,
    DragItem
  },
  props: {
    element: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      targets: []
    }
  },

  watch: {

  },
  created() {
  },
  methods: {
    onMove(e, originalEvent) {
      // this.moveId = e.draggedContext.element.id
      return true
    },
    end2(e) {},

    closeItem(tag) {
      const index = tag.index
      this.element.options.attrs.dragItems.splice(index, 1)
    }
  }
}

</script>
<style lang="scss" scoped>
  .filter-field {
    border-radius: 4px;
    height: 45px;

    .field-content {
      position: relative;
      display: table;
      width: 100%;
      height: 100%;
      white-space: nowrap;

      .field-content-left {
        width: 50px;
        max-width: 50px;
        position: relative;
        display: table-cell;
        vertical-align: middle;
        margin: 0px;
        padding: 8px;
        height: 100%;
        border-right: none;
        border: 1px solid var(--TableBorderColor, #E6E6E6);
        ;

        .field-content-text {
          box-sizing: border-box;
          overflow: hidden;
          overflow-x: hidden;
          overflow-y: hidden;
          word-break: break-all;
        }
      }

      .field-content-right {
        border-left: none;
        color: #9ea6b2;
        border: 1px solid var(--TableBorderColor, #E6E6E6);
        width: 0%;
        max-width: 0%;
        position: relative;
        display: table-cell;
        vertical-align: middle;
        margin: 0px;
        padding: 0 0 0 0;
        height: 100%;
      }
    }

  }
  .list-group-container:empty,.list-group-container>div:empty {
      display: none;
  }
  .list-group:empty,
  .list-group>div:empty {
    display: inline-block;
    width: 100%;
    height: calc(100% - 13px);
  }

  .list-group:empty:before,
  .list-group>div:empty:before {
    content: attr(data-value);
  }

    .blackTheme .theme-drag {
    background-color: var(--MainBG, #fff);
  }

</style>
