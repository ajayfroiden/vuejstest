<template>
    <div id="app">
        <div>
            <span v-for="(selectedValue, key) in selectedValues" v-bind:key="key" style="margin-right: 10px">
                {{selectedValue}} <span @click="removeSelectedValue(selectedValue)">x</span>
            </span>
            <input v-if="actionType == ''" @keyup="searchThisValue" v-model="searchValue" style="margin-left: 10px;border: white;border-bottom: 1px solid;" type="text"/>
        </div>
        <ul>
            <li v-for="(selectedValue, key) in selectedValues" v-bind:key="key">
                {{selectedValue}} <font-awesome-icon icon="check-circle" @click="removeSelectedValue(key)" />
            </li>
        </ul>
        <ul>
            <li style="margin-left: 10px" v-for="(dropdownList, key) in dropdownLists" v-bind:key="key">
                {{dropdownList.name}} <font-awesome-icon icon="circle" @click="valueSelected(dropdownList.name)" />
            </li>
        </ul>
    </div>
</template>

<script>
    import _ from 'lodash'; // eslint-disable-line

    export default {
        name: 'app',
        data () {
            return {
                dataResults : [
                    {
                        name : 'Category 1',
                        data : [
                            {
                                name : 'Sub Category 11 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 111',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 112',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 113',
                                        data: []
                                    }
                                ]
                            },
                            {
                                name : 'Sub Category 12 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 121',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 122',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 123',
                                        data: []
                                    }
                                ]
                            },
                            {
                                name : 'Sub Category 13 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 131',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 132',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 133',
                                        data: []
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        name : 'Category 2',
                        data : [
                            {
                                name : 'Sub Category 21 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 211',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 212',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 213',
                                        data: []
                                    }
                                ]
                            },
                            {
                                name : 'Sub Category 22 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 221',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 222',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 223',
                                        data: []
                                    }
                                ]
                            },
                            {
                                name : 'Sub Category 23 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 231',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 232',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 233',
                                        data: []
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        name : 'Category 3',
                        data : [
                            {
                                name : 'Sub Category 31 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 311',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 312',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 313',
                                        data: []
                                    }
                                ]
                            },
                            {
                                name : 'Sub Category 32 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 321',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 322',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 323',
                                        data: []
                                    }
                                ]
                            },
                            {
                                name : 'Sub Category 33 Item',
                                data: [
                                    {
                                        name: 'Sub Sub Category 331',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 332',
                                        data: []
                                    },
                                    {
                                        name: 'Sub Sub Category 333',
                                        data: []
                                    }
                                ]
                            }
                        ]
                    }
                ],
                dropdownLists : [],
                selectedValues: [],
                selectedTopArray: [],
                lastValue: '',
                actionType: '',
                searchValue: ''
            }
        },
        mounted () {
            this.dropdownLists = this.dataResults;
        },
        methods: {
            valueSelected (key) {
                this.selectedValues.push(key);
                this.lastValue = key;
                this.actionType = 'check';

                this.selectedTopArray = this.dropdownLists;


                let currentDropdownList = _.filter(this.dropdownLists, (dropdownList) => {
                    return dropdownList.name === key;
                });
                this.dropdownLists = currentDropdownList[0].data;
            },
            removeSelectedValue (key) {
                this.selectedValues = _.filter(this.selectedValues, (selectedValue) => {
                  return selectedValue != key;
                });

                if(this.selectedValues.slice(-1).pop() === undefined)
                {
                    this.dropdownLists = this.dataResults;
                    this.actionType = '';
                } else {
                    this.lastValue = this.selectedValues.slice(-1).pop();

                    this.dropdownLists = this.selectedTopArray;
                }
            },
            searchThisValue() {
                let currentDropdownList = _.filter(this.dropdownLists, (dropdownList) => {
                    return dropdownList.name.includes(this.searchValue);
                });
                if(currentDropdownList.length > 0)
                {
                    this.dropdownLists = currentDropdownList[0].data;
                }

                if(this.searchValue == '') {
                    this.dropdownLists = this.dataResults;
                }


                console.log(this.searchValue); // eslint-disable-line
            }
        }
    }
</script>

<style>

</style>
