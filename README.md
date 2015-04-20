# dropdown
js custom dropdown

<code>
/**
 * Dropdown
 **/
(function () {
	var app = window.app || {};
	var $items;

	/**
	 *
	 * @param selector string | domElement jquery селектор или dom element
	 * @param options object
	 */
	app.dropdown = function (selector, options) {
		if(_.isObject(options)) {
			_.extend(this.params, options);
		}
		if(_.isString(selector)) {
			$items = $(selector);
			_.each($items, function (item) {
				new app.dropdown(item, options);
			}, this);
			return false;
		}

		this.el = selector;
		this.$el = $(selector);
		this.$head = this.$el.find(this.params.selector.head_cnt);
		this.$cnt = this.$el.find(this.params.selector.cnt);

		this.$el.on('click', this.params.selector.head_cnt, this.onClickHead.bind(this));
	};

	app.dropdown.prototype = {
		params: {
			selector: {
				head: '.b-dropdown_head',
				head_cnt: '.b-dropdown_head_cnt',
				cnt: '.b-dropdown_cnt',
				hide: '.b-dropdown_cnt__hide',
				show: '.b-dropdown_cnt__show'
			}
		},
		onClickHead: function () {
			this.$cnt.toggle();
		}
	};

	window.app = app;
})();
</code>
