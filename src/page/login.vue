<template>
	<div class="login_page">
		<div class="login_left">
			<img src="../assets/img/bg.png" class="wave" alt="">
		</div>

		<div class="login_right">

			<transition name="form-fade" mode="in-out">
				<section class="form_contianer">
					<div class='titleArea rflex'>
						<img class="logo" src="../assets/img/avatar.svg" alt="">
						<span class='title'>后台管理系统</span>
					</div>
					<el-form :model="loginForm" :rules="rules" ref="loginForm" class="loginForm">
						<el-form-item prop="username" class="login-item">
							<span class="loginTips"><icon-svg icon-class="iconuser" /></span>
							<el-input @keyup.enter.native="submitForm('loginForm')" class="area" type="text" placeholder="用户名"
								v-model="loginForm.username"></el-input>
						</el-form-item>
						<el-form-item prop="password" class="login-item">
							<span class="loginTips"><icon-svg icon-class="iconLock" /></span>
							<el-input @keyup.enter.native="submitForm('loginForm')" class="area" type="password" placeholder="密码"
								v-model="loginForm.password"></el-input>
						</el-form-item>
						<el-form-item>
							<el-button type="primary" @click="submitForm('loginForm')" class="submit_btn">登录</el-button>
						</el-form-item>
						<div class="tiparea">
							<p class="wxtip">温馨提示：</p>
							<p class="tip">用户名为：admin/editor<span>(可用于切换权限)</span></p>
							<p class="tip">密码为：123456</p>
						</div>
						<div class="sanFangArea">
							<p class="title">第三方账号登录</p>
							<ul class="rflex">
								<li @click="loginByWechat">
									<icon-svg icon-class="iconwechat" />
								</li>
								<li>
									<icon-svg icon-class="iconweibo" />
								</li>
								<li>
									<icon-svg icon-class="iconGithub" />
								</li>
							</ul>
						</div>
					</el-form>
				</section>
			</transition>
		</div>
	</div>
</template>

<script>
import logoImg from "@/assets/img/logo.png";
import { login } from "@/api/user";
import { setToken } from '@/utils/auth'

export default {
	data() {
		return {
			logo: logoImg,
			loginForm: {
				username: 'admin',
				password: '123456'
			},
			rules: {
				username: [
					{ required: true, message: '请输入用户名', trigger: 'blur' },
					{ min: 2, max: 8, message: '长度在 2 到 8 个字符', trigger: 'blur' }
				],
				password: [
					{ required: true, message: '请输入密码', trigger: 'blur' },
					{min: 2, max: 8, message: '长度在 2 到 8 个字符', trigger: 'blur' }
				],
			}
		}
	},
	mounted() {
	},
	methods: {
		loginByWechat() {
		},
		showMessage(type, message) {
			this.$message({
				type: type,
				message: message
			});
		},
		submitForm(loginForm) {
			this.$refs[loginForm].validate((valid) => {
				if (valid) {
					let userinfo = this.loginForm;
					login(userinfo).then(res => {
						let userList = res.data.userList;
						setToken("Token", userList.token)
						this.$router.push({ path: '/' })
						this.$store.dispatch('initLeftMenu'); //设置左边菜单始终为展开状态
					})
				}
			});
		}
	}
}
</script>

<style lang="less" scoped>
.loginForm {
	/deep/ .el-input__inner {
	padding-left: 50px !important;
}
}


// .


.login_page {
	position: absolute;
	width: 100%;
	height: 100%;
	display: flex;
	flex-direction: row;
	align-items: center;

	.login_right {
		flex: 1;

		display: flex;
		justify-content: center;

	}

	.login_left {
		flex: 1;
		height: 100%;

		.wave {
			position: fixed;
			height: 100%;
			left: 0;
			bottom: 0;
			width: 100%;
			// z-index: -1;

		}
	}
}

.form_contianer {
	background: #fff;
	width: 370px;
	border-radius: 5px;
	padding: 25px;
	text-align: center;

	.titleArea {
		justify-content: center;
		align-items: center;
		text-transform: uppercase;
		font-size: 32px;
		width: 100%;
		padding-bottom: 20px;

		.logo {
			width: 40px;
			margin-right: 10px;
		}

		.title {

			color: #241d1d;
			font: 700 200%;

		}
	}

	.loginForm {
		.submit_btn {
			width: 100%;
			padding: 13px 0;
			font-size: 16px;
		}

		.loginTips {
			position: absolute;
			left: 10px;
			z-index: 20;
			// color: #FF7C1A;
			font-size: 18px;
			top: 50%;
			transform: translateY(-50%);
		}
	}
}

.manage_tip {
	margin-bottom: 20px;

	.title {
		font-family: cursive;
		font-weight: bold;
		font-size: 26px;
		color: #fff;
	}

	.logo {
		width: 60px;
		height: 60px;
	}
}

.tiparea {
	text-align: left;
	font-size: 12px;
	color: #4cbb15;
	padding: 10px 0;

	.tip {
		margin-left: 54px;
	}
}

.form-fade-enter-active,
.form-fade-leave-active {
	transition: all 1s;
}

.form-fade-enter,
.form-fade-leave-active {
	transform: translate3d(0, -50px, 0);
	opacity: 0;
}

// .loginForm{
// 	.el-button--primary{
// 		background-color:#FF7C1A;
// 		border:1px solid #FF7C1A;
// 	}
// }
.sanFangArea {
	border-top: 1px solid #DCDFE6;
	padding: 10px 0;
	display: none;

	.title {
		font-size: 14px;
		color: #8b9196;
		margin-bottom: 10px;
	}

	ul {
		li {
			flex: 1;
			display: flex;
			align-items: center;
			justify-content: center;
			cursor: pointer;

			.svg-icon {
				font-size: 24px;
			}
		}
	}
}

@media screen and (max-width: 968px) {
	.login_left {
		display: none;
	}

	.img {
		display: none;
	}

	.login-container {
		grid-template-columns: 1fr;
	}

	.login-box {
		justify-content: center;
	}
}</style>
