<template>
  <div class="wrap">
    <h1>ウマ娘レスボ計算機</h1>
    <div class="bonus">
      レースボーナス合計は <strong>{{bonus}}%</strong> です
    </div>
    <div class="useCard">
      <h2>使用するサポートカード</h2>
      <ul>
        <li v-for="(item, i) in model.cards" :key="`card-${i}`">
          <div class="cardItem">
            <h3>タイプ / レア度</h3>
            <div class="ts">
              <select v-model="model.types[i]" class="w45">
                <option v-for="type in types" :key="type" :value="type">
                  {{type}}
                </option>          
              </select>
              <select v-model="model.rs[i]" class="w45">
                <option v-for="re in rs" :key="re" :value="re">
                  {{re}}
                </option>          
              </select>
            </div>
          </div>

          <div class="cardItem">
            <h3>キャラクター {{i+1}}</h3>
            <div>
              <select v-model="model.cards[i]" class="w100">
                <template v-for="(spc, n) in cards">
                  <option v-if="spc.type === model.types[i] && spc.R === model.rs[i]" :key="`n-${n}`" :value="spc">
                    {{spc.name}} ({{spc.R}}・{{spc.type}})
                  </option>
                </template>         
              </select>
            </div>
          </div>
          <div class="cardItem">
            <h3>レベル</h3>
            <div>
              <select v-model="item.level" class="w100">
                <option v-for="(value,name) in item.levels" :key="value" :value="value">
                  {{ lv(name) }}
                </option>
              </select>
            </div>
            <div v-if="item.level" class="level">
              レースボーナス {{item.level}}%
              <span v-if="item.isUniq" class="uniq">固有あり</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
    <div class="reset">
      <button @click="reset">リセット</button>
    </div>
    <address><a href="https://github.com/baseball1989/RaceBonus">GitHub</a></address>
  </div>
</template>

<script>
//import { computed, defineComponent, reactive, watchEffect, onMounted } from 'vue'
import { reactive, computed } from 'vue'
import { cloneDeep } from 'lodash'
import cards from '@/assets/json/cards.json'

export default {
  name: 'RootPage',
  props: {
    msg: {
      type: String,
      required: false
    }
  },
  setup() {
    const model = reactive({
      cards: [
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
      ],
      types:[
        '',
        '',
        '',
        '',
        '',
        '',
      ],
      rs:[
        '',
        '',
        '',
        '',
        '',
        '',
      ],
    })

    const origin = {
      cards: [
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
        { 
          name: '',
          bonus: null,
          level: null,
          type: '',
          isUniq: false,
          isType: '',
          isR: '',
        },
      ],
      types:[
        '',
        '',
        '',
        '',
        '',
        '',
      ],
      rs:[
        '',
        '',
        '',
        '',
        '',
        '',
      ],
    }

    const reset = () => {
      model.cards = cloneDeep(origin.cards)
      model.types = cloneDeep(origin.types)
      model.rs = cloneDeep(origin.rs)
    }

    const types = [
      'スピード',
      'スタミナ',
      'パワー',
      '賢さ',
      '根性',
      '友人',
      'グループ',
    ]

    const rs =[
      'SSR',
      'SR',
      'R'
    ]

    const bonus = computed(()=>{
      return model.cards.reduce((sum,elm)=> sum + elm.level, 0)
    })

    const lv = (val) => {
      if(val === 'lv30') return '無凸'
      if(val === 'lv35') return '1凸'
      if(val === 'lv40') return '2凸'
      if(val === 'lv45') return '3凸'
      if(val === 'lv50') return '4凸'
    }

    document.title = 'ウマ娘レスボ計算機'

    return {
      model,
      cards,
      bonus,
      types,
      rs,
      lv,
      reset
    }
  }
}
</script>

<style lang="scss" scoped>
.cardItem {
  font-size: 1rem;
  margin-bottom: 16px;
  .ts {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
}
h1 {
  margin: 16px;
}
h1,h2 {
  text-align: center;
}
h2 {
  font-size: 1.2rem;
}
h3 {
  font-size: 1rem;
  margin: 0 0 8px;
}
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  list-style-type: none;
  padding: 0;
  margin: 0;
  text-align: left;
}
li {
  width: 350px;
  margin: 0 8px 24px 8px;
}
a {
  color: #42b983;
}
.bonus {
  text-align: center;
  position: sticky;
  top: 0;
  background: #efefef;
  padding: 8px;
  strong {
    font-size: 2rem;
  }
}
.level {
  text-align: center;
  margin-top: 8px;
  font-size: 1.1rem;
  font-weight: 800;
}
.w100 {
  width: 100%;
}
.w45 {
  width: 47.5%;
}
.uniq {
  background: orange;
  color:#fff;
  padding: 4px;
  border-radius: 4px;
  font-size: 0.6rem;

}
.reset {
  text-align: center;
  padding-bottom: 16px;
  position: sticky;
  bottom: 0;
  background: #fff;
}
select {
  padding: 8px;
}
address {
  margin-top: 16px;
  text-align: center;
}
</style>
