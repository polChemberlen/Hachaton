<template>
    <aside class="w-[321px] h-[100vh] bg-[#103D92] text-white flex flex-col pt-6 shadow-lg">

        <div class="text-4xl mx-auto font-krona mb-10">
            secret <br />manager<br />
        </div>

        <nav class="space-y-1 flex-grow relative">
            <div class="absolute left-0 top-0 w-[5px] h-full pointer-events-none">
                <div v-if="activeIndex !== -1" :style="{ top: `${activeIndex * itemHeight + navOffset + 10}px` }"
                    class="absolute w-full h-[40px] bg-white transition-all duration-300 z-10"></div>
            </div>
            <NuxtLink to="/secrets" class="flex items-center py-2 px-3" @mouseenter="hoveredIndex = 0">
                <svg width="50" height="40" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink">
                    <rect width="50" height="40" fill="url(#pattern0_160_277)" />
                    <defs>
                        <pattern id="pattern0_160_277" patternContentUnits="objectBoundingBox" width="1" height="1">
                            <use xlink:href="#image0_160_277" transform="matrix(0.00833333 0 0 0.0104167 0.1 0)" />
                        </pattern>
                        <image id="image0_160_277" width="96" height="96" preserveAspectRatio="none"
                            xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAABgCAYAAADimHc4AAAACXBIWXMAAAsTAAALEwEAmpwYAAADZElEQVR4nO3czUsVURjH8dOLIFgZlO0r2kRtJGpj2r/Q28peVr2gtowoFMRKFKVtbdpJ+6yIdGVtevkPKlqUtjMzEpffGDxB2D0zF713znmeeT4wIKn3/H5zr+eeuc2Mc8YYY4wxxhhjjDHGGLMesB04CpwFBoBbfhvw/3Yk+5n/ftFsHLADuAQ8A35RbBmYBi4CbbHziwXsA8b8Dt2o7HdHgY7YfcQAtgD9wBKN8wO4nj127H5JAzqAlzTPC2Bv7J5JAvYDH2m+L8Ch2H2TAhwEvte5A1eBOWAKeOC37OvX/nv1yMY6ELt3StPO5zp22rRfarYVrJjO+RVTkU/AHldlwNY65vx3QNcGHvsk8L7gsZ9X+o0Z6CvYQQ+Blk08fgvwqGCMa67C6/ylnB1zs4FjZUfLIYuVXBn5g6yQx00YL+8v4Z6rEv9muRzYGW83M+0UTEcfAmP+rNTHFsDlnFdjVxPH7c4Z94Kripxl4nQJY2crn1qeugp9pByafs6UMP75nGlom9POf2Zfy2oZ8zCwM+eI+bDTzh/N1jJXYoY3gQynnXbAjUD5qRIzPAlk6HfaAXcC5SdKzDAZyHDbaQcMB8oPVylDNCmUJ4EM0aRQngQyRJNCeRLIEE0K5UkgQzQplCeBDNGkUJ4EMkSTU372n1MNm73NVu4JANqB8QafcNVoS/4/itqdJsAJYB455oHjTtHOX0Ge3+KfBD/tLCDXgujpKPuADfnGnURAa8Eb7iv/BI1F3iZ8lrwzq1udNMCpnFK9LjFAb07ebieNP8e/5ivfJQqYCWTuc9IAQ4Eyoy5RrF1NU8uQk0bi4T4CM6sqg8DMqsogMLOqMgjMrKoMAjOrKoPAzKrKIDCzqjIIzKyqDAIzqyqDwMyqyiAws6oyCMysqgwCM6sqg8DMqsogMLOqMgjMrKoMAjOrKoPAzKrKIDCzqjIIzKyqDAIzqyqDwMyqyiAwcxAwqOi8oEEnDXA1UGbGyTsz7oqTxs4NjczfIiw7szhkBhgp8bqw0DaS88r/e1M/mbfEz5lTJbnrpAJ2C7s2bL2vwC4nGXBM6DViK0Cn08A/Cd+Q9crvdJr4C/bu+ze1VC1mN3EVP+3UcdfEnmxtzdqRZ+xrxIZ9lh6xqx1jjDHGGGOMMcYYY4wr9Aez4Sk3lcfIowAAAABJRU5ErkJggg==" />
                    </defs>
                </svg>
                <span class="ml-3 text-2xl font-medium">Секреты</span>
            </NuxtLink>

            <NuxtLink to="/projects" class="flex items-center py-2 px-3 " @mouseenter="hoveredIndex = 1">
                <svg width="50" height="40" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink">
                    <rect width="50" height="40" fill="url(#pattern0_160_282)" />
                    <defs>
                        <pattern id="pattern0_160_282" patternContentUnits="objectBoundingBox" width="1" height="1">
                            <use xlink:href="#image0_160_282" transform="matrix(0.00833333 0 0 0.0104167 0.1 0)" />
                        </pattern>
                        <image id="image0_160_282" width="96" height="96" preserveAspectRatio="none"
                            xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAABgCAYAAADimHc4AAAACXBIWXMAAAsTAAALEwEAmpwYAAADsElEQVR4nO3cT4hVdRTA8SMSlKTIRGDTYsBJo025E0MraVrYInQWKW1m0WI2Bc3GoTaim4SECA2aiRb9QcQWYrhpM6gQwQi2KJpAo0YR/FMDNv5Np6/86CcU/M5989688Xd+954PvM2b+y7n/M67b373/s69Is4555xzzjnnnHPOOeecc865NgCvAJ8CvwDX0P0FnAEOA8PAytyxFw1YC5ygc7PAh8CK3LkUB3gBmKE7poGXcudU2je/W4N/3x1gJHduRVjgz04rXwGP5s7R+j/cxfY78DbQDzyUO2dT4mwn5TawE+it+OwKYHP8lv+DXWEmNwWMAwNiSZxqpox2cCRdoQzHgTViQZzLp/R2sK8+4DRl+BPYtDij2t6gJS1gf48Anxj/SfpvEZ7q7oi2P2BJXdjvADCJfRPdGcnOByqpi/t/Hngf+B64APyNPS93K99OBihJagToDZOKOLNLGcsZXO0LcF8sQsqU5NKwAqxS0p3NGVRjCmAyX3MBNS1fcwE1LV9zATUtX3MBNS1fcwE1LV9zATUt324EBCwLp/Nx0WXU+Ks+BQAeAz4CrlK+wcUf7fQgJs3jcy8Cl6mXtx7MqP9/IJNafGZzxYWtkoVOjmdMFwB4HPiD+vrMegEOUG/TZgsALI/thylzwDfA3kJeWi/UNcsF2KFsfhd4VQpSkcuvlgvwtbL5ISkM8LmSy0GTBYjdDlqr+mtSkNCdFzsiUl63WoBtyqazoThSkNixkXLrgbfWt1GA0H5Yl5+fj5VcjuUIpmUB4iE7Y+KQXSBgCXBeyeVNqwXYUnHILpeCAOsrptGrrBZA66A+KoWJ5wApJ3MFVFkAYClwSdlsSApT0Q0+YrUA4cJbSmgx7JGChAttWr7AaqsF2K9s8q0UBnhPyeWHnEGpBYgzhnPKJsNSGOCUkssuqwXYUDFjeEIKAjxZcc/Cs1YL8IGpGcMCxPXqlN8kpxYFOKv8+R0pDDCh5LIvd2Cadcr74TDuk4IAPXG5MWVj7uA0e5T3J6UwwJCSy8VwnpM7OM1PyvvvSmGAI0ou47ljqyqA5mkpCP82jV1XctliIUBtjTflRykMMKjkEu6PftjytZGU3VIY4AvT6xjx+Qnz9ZyU9wykG0ou28X48lyd3TT1VK/48Iom+VIsCU8OqegSqOO3v1+sCU8OaUAR5oA3xKrw5JCKayaluwJslRLEu13GgJ/bPE+wJtw48l28M6ao1TvnnHPOOeecc84555xzzjnnnHNOnMg9Utd6JlTbfrUAAAAASUVORK5CYII=" />
                    </defs>
                </svg>
                <span class="ml-3 text-2xl font-medium">Проекты</span>
            </NuxtLink>

            <NuxtLink to="/requests" class="flex items-center py-2 px-3" @mouseenter="hoveredIndex = 2">
                <svg width="50" height="40" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink">
                    <rect width="50" height="40" fill="url(#pattern0_160_283)" />
                    <defs>
                        <pattern id="pattern0_160_283" patternContentUnits="objectBoundingBox" width="1" height="1">
                            <use xlink:href="#image0_160_283" transform="matrix(0.00833333 0 0 0.0104167 0.1 0)" />
                        </pattern>
                        <image id="image0_160_283" width="96" height="96" preserveAspectRatio="none"
                            xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAABgCAYAAADimHc4AAAACXBIWXMAAAsTAAALEwEAmpwYAAADsUlEQVR4nO3czW9VRRjH8TGQEDG8pIZFK6woOyBVKNiFhjcVti6oLHRlNVGokZa47cbWCCH8CVBAXasxbtxgi+66ckGoYIwvURRIVIy29kuGDElT75ze0/bOPOfc32fTNLk9fZ552rlzZp57nBMRERERERERERERERERERGbgJ3AOPADMEv9zYZcL/jccw/+W20y6DE+98Fcg/9SNKz2Mgf0px78NcBPuTM35Ec/JikLcCR3xgYdTlmA4dzZGjSUsgAjkSCuA1uTBVIuthG3TD63kGNLrr8SSY4mCyJDAcL1Ry0XIF0Q+QqQP3cTQUSoAJmhAuRFmxdgCngd2JwsmAWA1yKxDbhlALaE3KYsF2C+T4G9yYIKgE7g9oJY/PedbgmAp4HPmsjXXAEe+hDYkCw49yC+PcAE8Ef42ruEa2wEPiqRZ9ICDFDOTeApVxHAbuC7kjkOpAywC/i9ZIC3q1AEYBdwZwm5daYOtBf4EvizRKC/Ad3OKKC75B/Wv8Ckn/IsBL8W2A+cA+4VBH0VWOWMAVYDXy0y4D8DY8AzwOPOKr8MLViuecPOGOCdgnj/A94DHnNVAXQA30QS+tX/xzgj/MACtyKx/gO86KoovE/EzozfbPEydDK8Py06RwMnTKxuWiF0TDRyxcqNWLhXaORzV3VAT8EKYl3urQh/kwjMRH6mz9UBMB1J8FALflepzTLg+cjrv3V1AXwQSfJlAwV4JfL6cVcXwPuplqOUL0CsweBdVxfA6QoWYMzVRdgRrdoUdNHVBfB9JMmDBgrwXOT111wdAM8aX4auL1iG5u1+XgnAFxW+Ebvgqgw4TtwbVk7ECuKcWcppmgnAsTDNNPIL8KgzImylxzbj/IZih6sKP68DZ0PffMxJZwxwqiBev7W+xVkEPAJsAvYBZ8JWc5EJowcyq8JhUczf4bDpgH/jthBwH/B1wTTTyK3c3dNNdD/7Y9Nm/ZXlSDIcyt+lHH/W2uOMA55ssIpqJrd0h/IFa+2Y6SoM/oIi3CiZ46vOaGPWpdRzJiVPxArOCS6XyNNUZ5xfAX3sG5ySBdW61kR/rPrJIqs6MwWYCtNTV7Jg0jXnPhGubbo5V+3pKZgIIkIFyAwVIC/avAD6mKqBD2p31/iD2tsKWmySFmAoEkQ7eztlAfSwjv97IfXjavwjWiTH42pCEfqbuD1vB3PA0aSDP68Ig3pkGXkeWTavCDuA86H3px2KMRty9Tlvzzr4IiIiIiIiIiIiIiIiIiIi4qLuA7fxSw+pJ2eDAAAAAElFTkSuQmCC" />
                    </defs>
                </svg>
                <span class="ml-3 text-2xl font-medium">Заявки</span>
            </NuxtLink>


        </nav>

    </aside>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const hoveredIndex = ref(-1)
const itemHeight = 60 
const navOffset = 0 

const route = useRoute()
const activeIndex = computed(() => {
    if (route.path.startsWith('/secrets')) return 0
    if (route.path.startsWith('/projects')) return 1
    if (route.path.startsWith('/requests')) return 2
    if (route.path.startsWith('/operations')) return 3
    if (route.path.startsWith('/users')) return 4
    return -1
})
</script>

<style scoped></style>
